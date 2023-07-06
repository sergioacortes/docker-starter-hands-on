#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

ARG AspnetVersion=6.0-alpine
ARG SdkVersion=6.0-alpine

FROM mcr.microsoft.com/dotnet/aspnet:${AspnetVersion} AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:${SdkVersion} AS build

ARG BuildConfiguration=Relese

WORKDIR /src
COPY ["SampleAspNetMvcApp.csproj", "SampleAspNetMvcApp/"]
RUN dotnet restore "SampleAspNetMvcApp/SampleAspNetMvcApp.csproj"

WORKDIR "/src/SampleAspNetMvcApp"
COPY . .
RUN dotnet build "SampleAspNetMvcApp.csproj" --no-restore -c ${BuildConfiguration}

FROM build AS publish
RUN dotnet publish "SampleAspNetMvcApp.csproj" --no-build -c ${BuildConfiguration} -o /app/publish

FROM base AS final

ARG HttpPort=80
ENV ASPNETCORE_ENVIRONMENT=Production
ENV ASPNETCORE_URLS=http://+:$HttpPort

WORKDIR /app
RUN addgroup --gid 1000 a3software && adduser -G a3software -D -s /bin/false -u 1000 a3innuva
RUN chown -R a3innuva:a3software /app

COPY --from=publish /app/publish .
EXPOSE $HttpPort

ENTRYPOINT ["dotnet", "SampleAspNetMvcApp.dll"]