FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app 
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Chits.API.csproj","./"]
RUN dotnet restore "Chits.API.csproj"
COPY . .
RUN dotnet build "Chits.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Chits.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Chits.API.dll"]