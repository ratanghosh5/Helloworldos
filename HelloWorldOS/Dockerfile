FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["HelloWorldOS/HelloWorldOS.csproj", "HelloWorldOS/"]
RUN dotnet restore "HelloWorldOS/HelloWorldOS.csproj"
COPY . .
WORKDIR "/src/HelloWorldOS"
RUN dotnet build "HelloWorldOS.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorldOS.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorldOS.dll"]