FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 62210
EXPOSE 44306

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["AzureDevOpsWebApp/AzureDevOpsWebApp.csproj", "AzureDevOpsWebApp/"]
RUN dotnet restore "AzureDevOpsWebApp/AzureDevOpsWebApp.csproj"
COPY . .
WORKDIR "/src/AzureDevOpsWebApp"
RUN dotnet build "AzureDevOpsWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AzureDevOpsWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AzureDevOpsWebApp.dll"]