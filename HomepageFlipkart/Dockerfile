FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# copy csproj and restore as distinct layers
COPY ["HomepageFlipkart.csproj", "./"]
RUN dotnet restore "HomepageFlipkart.csproj"

# copy everything else and publish
COPY . .
RUN dotnet publish "HomepageFlipkart.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
ENV ASPNETCORE_URLS=http://+:80
EXPOSE 80

COPY --from=build /app/publish ./

ENTRYPOINT ["dotnet", "HomepageFlipkart.dll"]
