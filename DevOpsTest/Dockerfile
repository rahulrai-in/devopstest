FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY DevOpsTest/DevOpsTest.csproj DevOpsTest/
RUN dotnet restore DevOpsTest/DevOpsTest.csproj
COPY . .
WORKDIR /src/DevOpsTest
RUN dotnet build DevOpsTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DevOpsTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DevOpsTest.dll"]
