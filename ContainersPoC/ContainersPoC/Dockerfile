#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat
FROM microsoft/dotnet:2.2-sdk-nanoserver-1803 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:2.2-aspnetcore-runtime-nanoserver-1803
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "ContainersPoC.dll"]
