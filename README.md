# SQL-Covid-Portfolio
Select *
From [Portfolio Project]..['Covid Vaccinations$'];

Select * 
From [Portfolio Project]..['Covid Death$'];

Select * 
From [Portfolio Project]..['Covid Death$']
Order by 3,4

Select *
From [Portfolio Project]..['Covid Vaccinations$']
Order by 3,4

Select Location, date, total_cases, new_cases, total_deaths, population
From [Portfolio Project]..['Covid Vaccinations$']
Order by 1,2

---Looking at Total Cases VS Total Deaths

Select location, date, total_cases,population, (total_cases/population)*100 as Death_Percentage
From [Portfolio Project]..['Covid Vaccinations$']
Order by 1,2

select location,date,total_cases,population,(total_cases/population)*100 as Deathpercenttage
from [Portfolio Project]..['Covid Death$']
order by 1,2

select location,date,total_cases,population,(total_cases/population)*100 as Deathpercenttage
from [Portfolio Project]..['Covid Death$']
where location like '%states%'
order by 1,2

---Looking at Total Cases Vs Population
---% OF Population that had Covid

select location,date,population,total_cases,(total_cases/population)*100 as Deathpercenttage
from [Portfolio Project]..['Covid Death$']
where location like '%states%'
order by 1,2

---Countries mostly affected with Covid rate compare to Population

 Select location, population, Max(total_cases) as MostInfectedCount, Max (total_cases/population)*100 as PercentagePopulationInfected
 from [Portfolio Project]..['Covid Death$']
 group by Location, Population
 Order by 1,2

 --Where Location like '%state%'
 select location,date,total_cases,population,total_cases,(total_cases/population)*100 as Deathpercenttage
 from [Portfolio Project]..['Covid Death$']
 Where Location like '%states%'
 Order by 1,2

 3--where location like '%states%'
 Select location, population, Max(total_cases) as MostInfectedCount, Max (total_cases/population)*100 as PercentagePopulationInfected
 from [Portfolio Project]..['Covid Death$']
 group by Location, Population
 Order by PercentagePopulationInfected desc

 --showing countries with highest death count per population

 select location,max(cast( total_deaths as int))as totaldeathcount
 from [Portfolio Project]..['Covid Death$']
 where continent is not null
 group by location
 order by totaldeathcount desc


 
From [Portfolio Project]..['Covid Death$']
Where location like '%states%'
and continent is not null 
order by 1,2



--Show location by continent
 select location,max(cast( total_deaths as int))as totaldeathcount
 from [Portfolio Project]..['Covid Death$']
 where continent is  null
 group by  location
 order by totaldeathcount desc

 ----Population numbered
 Select SUM(new_cases) as total_cases, SUM(cast(new_deaths as int)) as total_deaths, SUM(cast(new_deaths as int))/SUM(New_Cases)*100 as DeathPercentage
From [Portfolio Project]..['Covid Death$']
where continent is not null 
--Group By date
order by 1,2

-- Total Population vs Vaccinations
-- Percentage of Population Vaccinated

Select thy.continent, thy.location, thy.date, thy.population, vac.new_vaccinations
, SUM(CONVERT(int,vac.new_vaccinations)) OVER (Partition by thy.Location Order by thy.location, thy.Date) as Vaccinated
--, (Vaccinated/population)*100
From [Portfolio Project]..['Covid Death$'] thy
Join [Portfolio Project]..['Covid Vaccinations$'] vac
	On thy.location = vac.location
	and thy.date = vac.date
where thy.continent is not null 
order by 2,3

2---Where Continent is not null
Select Location, SUM(cast(new_deaths as int)) as TotalDeathCount
From [Portfolio Project]..['Covid Death$']
---Where location like '%states%'
Where continent is not null 
and location not in ('World', 'European Union', 'International')
Group by Location
order by TotalDeathCount desc

---Where Continent is Null
Select Location, SUM(cast(new_deaths as int)) as TotalDeathCount
From [Portfolio Project]..['Covid Death$']
---Where location like '%states%'
Where continent is null 
and location not in ('World', 'European Union', 'International')
Group by Location
order by TotalDeathCount desc

-4--Location, Population, Date

Select location, population, date, Max(total_cases) as MostInfectedCount, Max (total_cases/population)*100 as PercentagePopulationInfected
 from [Portfolio Project]..['Covid Death$']
 --Where location like '%States%'
 Group by Location, Population, date
 Order by PercentagePopulationInfected desc
