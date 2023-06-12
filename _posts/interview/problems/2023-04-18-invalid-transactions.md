---
layout: post
published: true
title: "1169. Invalid Transactions"
categories: interview
tags: medium hashmap
---

> 유효하지 않을 가능성이 있는 트랜잭션 목록을 반환  
> - 금액이 $1000를 초과하거나
> - 다른 도시에서 동일한 이름으로 다른 거래가 발생한 후 60분 이내에 발생하는 경우  

[1169. Invalid Transactions](https://leetcode.com/problems/invalid-transactions/)

```java
class Solution {
    // 유효하지 않을 가능성이 있는 트랜잭션 목록을 반환
    // T: O(n^2)
    public List<String> invalidTransactions(String[] transactions) {
		List<String> invalid = new ArrayList<>();
        
		Map<String, List<Transaction>> map = new HashMap<>();

		/*
		 * build a map with name as key and value as list of transactions for that name
		 */
		for (String transaction : transactions) {
			Transaction tran = new Transaction(transaction);

			if (map.containsKey(tran.name)) {
				map.get(tran.name).add(tran);
			} else {
				List<Transaction> list = new ArrayList<>();
				list.add(tran);
				map.put(tran.name, list);
			}
		}

		for (String transaction : transactions) {
			Transaction tran = new Transaction(transaction);

			if (!isValid(map.get(tran.name), tran)) {
				invalid.add(transaction);
			}
		}

		return invalid;
	}

	public boolean isValid(List<Transaction> transactions, Transaction transaction) {

		/* if there is only one transaction and the amount is less than 1000 */
		if (transactions.size() <= 1 && transaction.amount < 1000)
			return true;

		/* check against all other transaction to check it this one is valid */
		for (Transaction tran : transactions) {
			if (transaction.invalidTransaction(tran.city, tran.time)) {
				return false;
			}
		}
        
		return true;
	}

	class Transaction {
		String name;
		int time;
		int amount;
		String city;

		Transaction(String transaction) {
			String[] t = transaction.split(",");
			this.name = t[0];
			this.time = Integer.parseInt(t[1]);
			this.amount = Integer.parseInt(t[2]);
			this.city = t[3];
		}

		public boolean invalidTransaction(String city, int time) {
			return invalidAmount() || differentCity(city, time);
		}

        // 다른 도시에서 같은 이름의 거래가 60분 이내에 발생했는지 검사
		private boolean differentCity(String city, int time) {
			return !this.city.equals(city) && Math.abs(this.time - time) <= 60;
		}

		private boolean invalidAmount() {
			return this.amount > 1000;
		}
	}
}
```