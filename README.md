# CRM 
from multiprocessing import Pool
from collections import Counter
from functools import reduce
def map_reduce(input_data, num_processes=4):
    chunks = (chunk.split() for chunk in input_data.splitlines() if chunk.strip())
    with Pool(num_processes) as pool:
        intermediate_result = pool.map(Counter, chunks)
        final_result = reduce(lambda x,y: x + y, intermediate_result)
    return final_result
if __name__ == '__main__':
    input_data = """
    I am a student of class 9
    I study economics and biology
    my favourite subject is French
    """
    result = map_reduce(input_data)
    print(result)

apripori
from mlxtend.preprocessing import TransactionEncoder
from mlxtend.frequent_patterns import apriori, association_rules
import pandas as pd
transactions = [
    ['Butter', 'Eggs', 'Milk'],
    ['Milk', 'Bread'],
    ['Milk', 'Butter', 'Bread'],
    ['Bread', 'Eggs']
]
te = TransactionEncoder()
te_ary =  te.fit(transactions).transform(transactions)
df = pd.DataFrame(te_ary, columns= te.columns_)
frequent_itemsets = apriori(df, min_support=0.2, use_colnames=True)
rules = association_rules(frequent_itemsets, metric="confidence", min_threshold=0.7)
print(frequent_itemsets)
print(rules)

pagerank
import networkx as nx
def page_rank(graph):
    return nx.pagerank(graph)
if __name__ == '__main__':
    edges = [
        ('A','B'), ('A','C'),
        ('B','A'), ('B','C'),
        ('C', 'A')
    ]
    G = nx.DiGraph()
    G.add_edges_from(edges)
    ranks = page_rank(G)
    print("Page Rank")
    for node, rank in ranks.items():
        print(f"{node}:{rank}")

bloom
from pybloom_live import ScalableBloomFilter
bloom_filter = ScalableBloomFilter()
elements_to_add = ['bunty', 'prem', 'yash']
for element in elements_to_add:
    bloom_filter.add(element)
elements_to_check = ['bunty', 'orange', 'apple']
for element in elements_to_check:
    if element in bloom_filter:
        print(f"{element} is present")
    else:
        print(f"{element} is not present")
