FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY TestJenkins/TestJenkins.csproj TestJenkins/
RUN dotnet restore TestJenkins/TestJenkins.csproj
COPY . .
WORKDIR /src/TestJenkins
RUN dotnet build TestJenkins.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TestJenkins.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestJenkins.dll"]
