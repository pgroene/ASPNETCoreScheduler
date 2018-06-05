FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 34929
EXPOSE 44376

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ASPNETCoreScheduler/ASPNETCoreScheduler.csproj ASPNETCoreScheduler/
RUN dotnet restore ASPNETCoreScheduler/ASPNETCoreScheduler.csproj
COPY . .
WORKDIR /src/ASPNETCoreScheduler
RUN dotnet build ASPNETCoreScheduler.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ASPNETCoreScheduler.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ASPNETCoreScheduler.dll"]
