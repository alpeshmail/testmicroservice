FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TestCoreApplication/TestCoreApplication.csproj", "TestCoreApplication/"]
RUN dotnet restore "TestCoreApplication/TestCoreApplication.csproj"
COPY . .
WORKDIR "/src/TestCoreApplication"
RUN dotnet build "TestCoreApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestCoreApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestCoreApplication.dll"]