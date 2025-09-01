FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY SampleAPI/*.csproj ./SampleAPI/
COPY *.sln ./
RUN dotnet restore ./SampleAPI/SampleAPI.csproj
COPY SampleAPI/. ./SampleAPI/
WORKDIR /src/SampleAPI
RUN dotnet publish -c Release -o /app/publish --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
EXPOSE 80
ENTRYPOINT ["dotnet", "SampleAPI.dll"]
