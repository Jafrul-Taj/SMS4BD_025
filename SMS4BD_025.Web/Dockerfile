FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["SMS4BD_025.Web/SMS4BD_025.Web.csproj", "SMS4BD_025.Web/"]
RUN dotnet restore "SMS4BD_025.Web/SMS4BD_025.Web.csproj"
COPY . .
WORKDIR "/src/SMS4BD_025.Web"
RUN dotnet build "SMS4BD_025.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SMS4BD_025.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SMS4BD_025.Web.dll"]