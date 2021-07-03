#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["PracticeCheck_/PracticeCheck_.csproj", "PracticeCheck_/"]
RUN dotnet restore "PracticeCheck_/PracticeCheck_.csproj"
COPY . .
WORKDIR "/src/PracticeCheck_"
RUN dotnet build "PracticeCheck_.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PracticeCheck_.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PracticeCheck_.dll"]