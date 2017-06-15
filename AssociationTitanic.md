## Association Example Using Titanic Data Set

### https://www.youtube.com/watch?v=DQGJhZNhG4M
### https://github.com/A01203249/YouTube-Videos/tree/master/R_code_%26_data

### adjust this line to the folder where you will be saving this code and the data file

load("C:/Users/ed.orlando07/Desktop/AssociationTitanic/titanic.raw.rdata")
head(titanic.raw)
attach(titanic.raw)

### if not done so.....
### install.packages(Matrix) using Tools | Install Packages
### install.packages(arules) using Tools | Install Packages

library(arules) 
  ### run this code everytime
  ### this is calling the library
  ### which is different than installing it
  ### installs happen once, calling libraries happen every time.

?apriori
  ### Gives you more information on apriori

### find association rules with default settings
rules = apriori(titanic.raw)
inspect(rules)

#Line 4 of the data set description
#19.3% of the cases have Adult and Female.
#90.4% is the confidence level of the association.  Out of the number of females, 90.4% of them were adults
#Lift is the measure of the performance against the target model

#In computer science and data mining, Apriori is a classic algorithm for learning association rules. 
#Apriori is designed to operate on databases containing transactions. As is common in association rule mining, 
#given a set of itemsets, the algorithm attempts to find subsets which are common to at least a minimum number 
#C of the itemsets. Apriori uses a "bottom up" approach, where frequent subsets are extended one item at a time 
#(a step known as candidate generation), and groups of candidates are tested against the data. The algorithm 
#terminates when no further successful extensions are found.

#Apriori uses breadth-first search and a tree structure to count candidate item sets efficiently. 
#It generates candidate item sets of length k from item sets of length k-1. Then it prunes the 
#candidates which have an infrequent sub pattern. According to the downward closure lemma, the 
#candidate set contains all frequent k-length item sets. After that, it scans the transaction 
#database to determine frequent item sets among the candidates.

#Apriori, while historically significant, suffers from a number of inefficiencies or trade-offs, 
#which have spawned other algorithms. Candidate generation generates large numbers of subsets 
#(the algorithm attempts to load up the candidate set with as many as possible before each scan). 
#Bottom-up subset exploration (essentially a breadth-first traversal of the subset lattice) finds 
#any maximal subset S only after all 2^{|S|}-1 of its proper subsets.

#We then set rhs=c("Survived=No", "Survived=Yes") in appearance to make sure that only "Survived=No" 
#and "Survived=Yes" will appear in the rhs of rules.

#Rules with rhs containing "Survived" only
rules <- apriori(titanic.raw, parameter = list(minlen=2, supp=0.005, conf=0.8), appearance = list(rhs=c("Survived=No", "Survived=Yes"), default="lhs"), control = list(verbose=F))
rules.sorted <- sort(rules, by="lift")
inspect(rules.sorted)
