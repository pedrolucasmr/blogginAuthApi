FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["BlogginAuthApi/BlogginAuthApi.csproj", "BlogginAuthApi/"]
RUN dotnet restore "BlogginAuthApi/BlogginAuthApi.csproj"
COPY . .
WORKDIR "/src/BlogginAuthApi"
RUN dotnet build "BlogginAuthApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BlogginAuthApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BlogginAuthApi.dll"]
