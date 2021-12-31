FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
# copy  csproj files into respective folder
COPY ["./PaymentApi/PaymentApi.csproj", "src/PaymentApi/"]
# run restore over API project - this pulls restore over the dependent projects as well
RUN dotnet restore "src/PaymentApi/PaymentApi.csproj"
COPY . .
# run build over the API project
WORKDIR "/src/PaymentApi/"
RUN dotnet build -c Release -o /app/build
# run publish over the API project
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish
FROM base AS runtime
WORKDIR /app
COPY --from=publish /app/publish .
RUN ls -l
ENTRYPOINT [ "dotnet", "PaymentApi.dll" ]