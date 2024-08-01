# Gene_Expression_Database_MySQL
# Bioinformatics Gene Expression Project

This project is designed to manage and analyze gene expression data using MySQL. It includes the creation of tables for genes, experiments, and expression levels, as well as sample data and queries to retrieve meaningful insights.

## Table of Contents

•  [Database Schema](#database-schema)

•  [Sample Data](#sample-data)

•  [Queries](#queries)

•  [Verification](#verification)

•  [Usage](#usage)


## Database Schema

The database schema consists of three tables: `Genes`, `Experiments`, and `ExpressionLevels`.

### Genes Table

```sql
CREATE TABLE Genes (
GeneID INT AUTO_INCREMENT PRIMARY KEY,
GeneName VARCHAR(100) NOT NULL,
Organism VARCHAR(50)
);

Experiments Table
CREATE TABLE Experiments (
ExperimentID INT AUTO_INCREMENT PRIMARY KEY,
ExperimentName VARCHAR(100) NOT NULL,
Date DATE
);

ExpressionLevels Table
CREATE TABLE ExpressionLevels (
ExpressionID INT AUTO_INCREMENT PRIMARY KEY,
GeneID INT,
ExperimentID INT,
ExpressionLevel DECIMAL(5, 2),
Significance DECIMAL(5, 2),
FOREIGN KEY (GeneID) REFERENCES Genes(GeneID),
FOREIGN KEY (ExperimentID) REFERENCES Experiments(ExperimentID)
);

Sample Data
The following sample data is inserted into the tables:

Insert Data into Genes Table
INSERT INTO Genes (GeneName, Organism) VALUES
('BRCA1', 'Human'),
('TP53', 'Human'),
('CFTR', 'Human');

Insert Data into Experiments Table
INSERT INTO Experiments (ExperimentName, Date) VALUES
('Cancer Study 1', '2024-01-15'),
('Cancer Study 2', '2024-02-20'),
('Genetic Disorder Study', '2024-03-10');

Insert Data into ExpressionLevels Table
INSERT INTO ExpressionLevels (GeneID, ExperimentID, ExpressionLevel, Significance) VALUES
(1, 1, 2.5, 0.01),
(1, 2, 3.0, 0.05),
(2, 1, 1.8, 0.02),
(2, 3, 2.2, 0.03),
(3, 2, 1.5, 0.04),
(3, 3, 2.0, 0.01);

Queries
List All Genes with Their Expression Levels in Each Experiment
SELECT Genes.GeneName, Experiments.ExperimentName, ExpressionLevels.ExpressionLevel, ExpressionLevels.Significance
FROM ExpressionLevels
JOIN Genes ON ExpressionLevels.GeneID = Genes.GeneID
JOIN Experiments ON ExpressionLevels.ExperimentID = Experiments.ExperimentID;

Find Genes with Significant Expression Levels (p-value < 0.05)
SELECT Genes.GeneName, Experiments.ExperimentName, ExpressionLevels.ExpressionLevel, ExpressionLevels.Significance
FROM ExpressionLevels
JOIN Genes ON ExpressionLevels.GeneID = Genes.GeneID
JOIN Experiments ON ExpressionLevels.ExperimentID = Experiments.ExperimentID
WHERE ExpressionLevels.Significance < 0.05;

Get the Average Expression Level of Each Gene Across All Experiments
SELECT Genes.GeneName, AVG(ExpressionLevels.ExpressionLevel) AS AverageExpression
FROM ExpressionLevels
JOIN Genes ON ExpressionLevels.GeneID = Genes.GeneID
GROUP BY Genes.GeneName;

Count the Number of Experiments Each Gene is Involved In
SELECT Genes.GeneName, COUNT(ExpressionLevels.ExperimentID) AS NumberOfExperiments
FROM ExpressionLevels
JOIN Genes ON ExpressionLevels.GeneID = Genes.GeneID
GROUP BY Genes.GeneName;

Verification
Verify Table Creation
SHOW TABLES;

DESCRIBE Genes;
DESCRIBE Experiments;
DESCRIBE ExpressionLevels;

Verify Data Insertion
SELECT * FROM Genes;
SELECT * FROM Experiments;
SELECT * FROM ExpressionLevels;

Usage
1. 
Create the Database and Tables:

CREATE DATABASE BioinformaticsDB;
USE BioinformaticsDB;
-- (Create tables as shown above)

1. 
Insert Sample Data:

-- (Insert data as shown above)

1. 
Run Queries:

-- (Run queries as shown above)
