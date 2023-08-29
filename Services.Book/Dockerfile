FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Services.Book/Services.Book.csproj", "Services.Book/"]
RUN dotnet restore "Services.Book/Services.Book.csproj"
COPY . .
WORKDIR "/src/Services.Book"
RUN dotnet build "Services.Book.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Services.Book.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Services.Book.dll"]
