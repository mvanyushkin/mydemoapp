FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["/MyDemoApp.csproj", "MyDemoApp/"]
RUN file="$(ls -l)" && echo $file
RUN dotnet restore "MyDemoApp/MyDemoApp.csproj"
COPY . "MyDemoApp" 
WORKDIR "/src/MyDemoApp"
RUN dotnet build "MyDemoApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MyDemoApp.csproj" -c Release -o /app/publish


FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyDemoApp.dll"]
