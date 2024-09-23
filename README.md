# SQL_project
codes used for the SQL project using the election database 

Solutions codes

1. 
-- To determine which state has the highest and lowest number of local government areas

WITH lga_state AS (
		SELECT 
		lga_tbl.lga_id,
		lga_tbl.lga_name,
		state_tbl.state_name
		FROM lga_tbl
		INNER JOIN state_tbl ON lga_tbl.state_id = state_tbl.state_id
)
SELECT 
		state_name,
		count(state_name) AS sum_lga
FROM 
		lga_state
GROUP BY
		state_name
ORDER BY
	sum_lga DESC;
-- the result can be ordered by ASC to determine which state has the lowest lga


2. 
--to determine which state is the most populated

WITH lga_state_pop AS (
		SELECT  
		state_tbl.state_name,
		population.population
		FROM 
		state_tbl
		INNER JOIN 
		lga_tbl on state_tbl.state_id = lga_tbl.state_id
		INNER JOIN population on
		population.lga_id = lga_tbl.lga_id
		)
SELECT 
		state_name,
		sum(population) AS pop_sum
FROM lga_state_pop
GROUP BY
		state_name
ORDER by
		pop_sum DESC;

--lagos state with a 14496749 has the highest population

3. 
-- To determine which senatorial area has the highest number of local government areas

WITH lga_senatorial AS (
		SELECT
		lga_tbl.lga_name,
		lga_tbl.representative_district_id as lga_district,
		senatorial_district_tbl .district_id as senatorial_district,
		senatorial_district_tbl .district_name as senatorial_district_name
		FROM 
		senatorial_district_tbl
		INNER JOIN 
		lga_tbl  ON senatorial_district_tbl.state_id = lga_tbl .state_id
)

SELECT
		senatorial_district,
		senatorial_district_name,
		count(lga_district) AS lga_count
FROM
		lga_senatorial
GROUP BY
		senatorial_district
ORDER BY
		lga_count DESC;
![image](https://github.com/user-attachments/assets/eaa00865-c5c9-42b6-8411-267ce877af23)
