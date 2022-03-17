#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

#FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
#WORKDIR /app
#EXPOSE 80
#EXPOSE 443

#FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
#WORKDIR /src
#COPY ["DNAzure-FirstWebApi/DNAzure-FirstWebApi.csproj", "DNAzure-FirstWebApi/"]
#RUN dotnet restore "DNAzure-FirstWebApi/DNAzure-FirstWebApi.csproj"
#COPY . .
#WORKDIR "/src/DNAzure-FirstWebApi"
#RUN dotnet build "DNAzure-FirstWebApi.csproj" -c Release -o /app/build

#FROM build AS publish
#RUN dotnet publish "DNAzure-FirstWebApi.csproj" -c Release -o /app/publish

#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "DNAzure-FirstWebApi.dll"]

####################################

FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "DNAzure-FirstWebApi.dll"]