FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Host/Host.csproj", "Host/"]
COPY ["IdentityServer.ActiveDirectory/IdentityServer.ActiveDirectory.csproj", "IdentityServer.ActiveDirectory/"]
RUN dotnet restore "Host/Host.csproj"
COPY . .
WORKDIR "/src/Host"
RUN dotnet build "Host.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Host.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Host.dll"]