FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY PipelineTests/PipelineTests.csproj PipelineTests/
RUN dotnet restore PipelineTests/PipelineTests.csproj
COPY . .
WORKDIR /src/PipelineTests
RUN dotnet build PipelineTests.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish PipelineTests.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PipelineTests.dll"]
