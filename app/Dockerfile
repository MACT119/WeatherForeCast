FROM alpine:latest  
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY ./ ./
CMD ["./app"]  

# https://hub.docker.com/_/microsoft-dotnet
FROM mcr.microsoft.com/dotnet/sdk:5.0
WORKDIR /source

# copy csproj and restore as distinct layers
WORKDIR /app
#COPY *.sln .
COPY *.csproj ./
RUN dotnet restore

# copy everything else and build app
COPY /. ./
WORKDIR /source/weatherforecast
RUN dotnet publish -c release -o /app --no-restore

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "weatherforecast.dll"]