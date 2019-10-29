FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["LinuxKuberPoC.csproj", "LinuxKuberPoC/"]

RUN dotnet restore "LinuxKuberPoC.csproj"
COPY . .
WORKDIR "/src/LinuxKuberPoC"
RUN dotnet build "LinuxKuberPoC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LinuxKuberPoC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "LinuxKuberPoC.dll"]