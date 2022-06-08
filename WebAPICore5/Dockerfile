#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 
#AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 
#AS build
WORKDIR /src
COPY ["WebAPICore5.csproj", ""]
RUN dotnet restore "./WebAPICore5.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "./WebAPICore5.csproj" -c Release -o /app/build
#LABEL "MACT:Termino el BUILD"

#FROM mcr.microsoft.com/dotnet/sdk:5.0 
#AS publish
RUN dotnet publish "./WebAPICore5.csproj" -c Release -o /app/publish
#LABEL "MACT:Termino el PUBLISH-MACT"
COPY ./ .

FROM mcr.microsoft.com/dotnet/aspnet:5.0
#FROM base
#AS final
WORKDIR /app/publish
COPY ./ .

WORKDIR /app
#COPY --from=publish /app/publish .
EXPOSE 80
EXPOSE 443
ENTRYPOINT ["dotnet", "WebAPICore5.dll"]