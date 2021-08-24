FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["CNProjetosG/CNProjetosG.csproj", "CNProjetosG/"]
RUN dotnet restore "CNProjetosG/CNProjetosG.csproj"
COPY . .
WORKDIR "/src/CNProjetosG"
RUN dotnet build "CNProjetosG.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "CNProjetosG.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "CNProjetosG.dll"]
