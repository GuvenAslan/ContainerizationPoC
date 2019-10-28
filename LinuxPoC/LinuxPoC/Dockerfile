FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["LinuxPoC.csproj", "LinuxPoC/"]
RUN dotnet restore "LinuxPoC.csproj"
COPY . .
WORKDIR "/src/LinuxPoC"
RUN dotnet build "LinuxPoC.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "LinuxPoC.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LinuxPoC.dll"]