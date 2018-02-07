FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY *.sln ./
COPY ClassLibrary1/ClassLibrary1.csproj ClassLibrary1/
COPY WebApplication120/WebApplication120.csproj WebApplication120/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/WebApplication120
RUN dotnet build WebApplication120.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebApplication120.csproj -c Release -o /app

FROM base AS final
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApplication120.dll"]
