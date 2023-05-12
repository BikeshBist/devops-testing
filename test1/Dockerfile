# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:7.0.102 AS build
WORKDIR /build3

RUN curl -sL https://deb.nodesource.com/setup_16.x |  bash -
RUN apt-get install -y nodejs

# copy csproj and restore as distinct layers
COPY ./Code/Websites/DanpheEMR/*.csproj .
RUN dotnet restore

# copy everything else and build app
COPY . .
WORKDIR /build3
RUN dotnet publish -c release -o published --no-cache

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:6.0
WORKDIR /app
COPY --from=build /build3/published ./
ENTRYPOINT ["dotnet", "DanpheEMR.dll"]

/Code/Websites/DanpheEMR