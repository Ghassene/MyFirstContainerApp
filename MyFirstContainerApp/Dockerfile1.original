FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["MyFirstContainerApp/MyFirstContainerApp.csproj", "MyFirstContainerApp/"]
RUN dotnet restore "MyFirstContainerApp/MyFirstContainerApp.csproj"
COPY . .
WORKDIR "/src/MyFirstContainerApp"
RUN dotnet build "MyFirstContainerApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyFirstContainerApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyFirstContainerApp.dll"]