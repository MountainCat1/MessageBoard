﻿FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["MessageBoardApp/MessageBoardApp.csproj", "MessageBoardApp/"]
RUN dotnet restore "MessageBoardApp/MessageBoardApp.csproj"
COPY . .
WORKDIR "/src/BaseApp"
RUN dotnet build "MessageBoardApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MessageBoardApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AccountApp.dll"]
