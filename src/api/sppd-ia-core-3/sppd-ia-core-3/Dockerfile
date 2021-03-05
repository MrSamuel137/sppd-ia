#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["sppd-ia-core-3.csproj", "."]
RUN dotnet restore "./sppd-ia-core-3.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "sppd-ia-core-3.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "sppd-ia-core-3.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "sppd-ia-core-3.dll"]