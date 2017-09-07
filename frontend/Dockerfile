FROM microsoft/aspnetcore-build:2 AS develop
EXPOSE 80
WORKDIR /src
COPY *.sln ./
COPY sharedlib/*.csproj sharedlib/
COPY frontend/*.csproj frontend/
RUN dotnet restore
COPY . .
WORKDIR frontend

FROM develop AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish -c $BUILD_CONFIGURATION -o /app

FROM microsoft/aspnetcore:2 AS release
EXPOSE 80
WORKDIR /app
COPY --from=publish /app .
CMD ["dotnet", "frontend.dll"]
