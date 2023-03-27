FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5110

ENV ASPNETCORE_URLS=http://+:5110

# Creates a non-root user with an explicit UID and adds permission to access the /app folder
# For more info, please refer to https://aka.ms/vscode-docker-dotnet-configure-containers
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
USER appuser

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["./HelloWorldWebApp.csproj", "HelloWorldWebApp/"]
RUN dotnet restore "HelloWorldWebApp/HelloWorldWebApp.csproj"
COPY . .
WORKDIR "/src/HelloWorldWebApp"
RUN dotnet build "HelloWorldWebApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "HelloWorldWebApp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "HelloWorldWebApp.dll"]
