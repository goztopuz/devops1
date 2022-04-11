#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Shopping2.Client/Shopping2.Client.csproj", "Shopping2.Client/"]
RUN dotnet restore "Shopping2.Client/Shopping2.Client.csproj"
COPY . .
WORKDIR "/src/Shopping2.Client"
RUN dotnet build "Shopping2.Client.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shopping2.Client.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Shopping2.Client.dll"]