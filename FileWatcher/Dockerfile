FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["FileWatcher/FileWatcher.fsproj", "FileWatcher/"]
RUN dotnet restore "FileWatcher/FileWatcher.fsproj"
COPY . .
WORKDIR "/src/FileWatcher"
RUN dotnet build "FileWatcher.fsproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "FileWatcher.fsproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "FileWatcher.dll"]
