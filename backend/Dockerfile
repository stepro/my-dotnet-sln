FROM microsoft/aspnetcore:2 AS base
EXPOSE 80
WORKDIR /app

FROM microsoft/aspnetcore-build:2 AS build
WORKDIR /src
COPY my-dotnet-sln.sln .
COPY backend/backend.csproj backend/
COPY sharedlib/sharedlib.csproj sharedlib/
RUN dotnet restore backend/backend.csproj
COPY . .
WORKDIR backend

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish --no-restore -c $BUILD_CONFIGURATION -o /app

FROM base AS release
COPY --from=publish /app .
CMD ["dotnet", "backend.dll"]
