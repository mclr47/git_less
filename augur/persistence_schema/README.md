# README for Augur Schema

## Steps to just Make the database
1. Create a user called "augur" in your postgresql version 10 or higher database system. 
2. Execute the file name `new-augur.0.0.77.5-release.sql` as the `augur` user, if you have granted that user schema creation privileges, or as any other user who has schema creation privileges.  All schemas, the tables, and sequences they contain, are owned by the `augur` user. Sure, you could do a search and replace and make everything owned by `Sarah`, but why would you do that? 

## Augur Data
The `augur_data` schema contains *most* of the information analyzed and constructed by Augur. The origin's of the data inside of augur are: 
1. `workers/augur_github_worker`: Pulls data from the GitHub API. Presently this is focused on issues, including issue_comments, issue_events, issue_labels and contributors. Note that all messages are stored in Augur in the `messages` table. This is to facilitate easy analysis of the tone and characteristics of text communication in a project from one place. 
2. `workers/facade_worker`: Based on http://www.github.com/brianwarner/facade, but substantially modified in the fork located at http://github.com/sgoggins/facade. The modifications include modularization of code, connections to Postgresql data instead of MySQL and other changes noted in the commit logs. 
3. `workers/insight_worker`: Generates summarizations from raw data gathered from commits, issues, and other info. 
4. `workers/linux_badge_worker`: Pulls data from the Linux Foundation's badging program. 
5. `workers/code_analysis`: Populates the table `repo_labor` using the "SCC" tool provided the https://github.com/boyter/scc project. This worker is presently in development and not deployed. 

## Augur Operations 
The `augur_operations` tables are where most of the operations tables are going to exist. There are a few, like `settings` that remain in `augur_data` for now, but will be moved. They keep records related to analytical history and data provenance for data in the schema. They also store information including API keys. 

## SPDX 
The `spdx` schema serves the storage for software bill of materials and license declarations scans on projects, conducted using this fork of the DoSOCSv2 project: https://github.com/Nebrethar/DoSOCSv2 

## Types of files: 
1. SQL Files are used to build the database directly. 
2. The PDF is a readable version of the full data model

