FROM microsoft/aspnetcore-build:1.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
ENV ASPNETCORE_URLS=http://+:8123
EXPOSE 8123
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/aspnetcore:1.1
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "aspnet-core-dotnet-core.dll"]
