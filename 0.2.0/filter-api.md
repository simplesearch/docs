
```
/**
	 * FilterQuery、BooleanQuery支持写出很复杂的filter来，支持链式写法，支持bool层层嵌套
	 */
	@Test
	public void test_filterAll(){
		filter_test1();//中等复杂
		filter_test2();//特别复杂
	}
	
	void filter_test1(){
		BooleanQuery bool = BooleanQuery.bool();
		FilterQuery filter = FilterQuery.fq(bool);
		
		bool.must(
				BooleanQuery.bool()
					.must(QueryBuilders.term("cid", "1"))
					.should(QueryBuilders.term("cityid", "1"))
				)
			.must(
				BooleanQuery.bool()
					.must(QueryBuilders.term("cityid", "1"))
					.should(QueryBuilders.term("cityid", "1"))
			)
			.must_not(BooleanQuery.bool().must(QueryBuilders.term("cid", "1")))
			.should(BooleanQuery.bool().must(QueryBuilders.term("cid", "1")));
		System.out.println(filter.toString());
	}
	
	void filter_test2(){
		BooleanQuery bool = BooleanQuery.bool();
		FilterQuery filter = FilterQuery.fq(bool);
		
		//复杂bool查询测试
		bool.must(
				BooleanQuery.bool()
					.must(
						BooleanQuery.bool()
						.must(
							BooleanQuery.bool()
								.must(QueryBuilders.term("cid", "1"))
								.should(QueryBuilders.term("cid", "1"))
								.must_not(QueryBuilders.term("cid", "1"))
								.must(QueryBuilders.term("cid2", "2"))
						)
						.should(QueryBuilders.term("cid", "1"))
						.must_not(QueryBuilders.term("cid", "1"))
						.must(QueryBuilders.term("cid2", "2"))
					)
					.must_not(
						BooleanQuery.bool().must(QueryBuilders.term("cid", "1"))
						.should(QueryBuilders.term("cid", "1"))
						.must_not(QueryBuilders.term("cid", "1"))
						.must(QueryBuilders.term("cid2", "2"))
					)
					.should(BooleanQuery.bool().must(QueryBuilders.term("cid", "1")))
				)
			.must_not(
				BooleanQuery.bool()
					.must(
						BooleanQuery.bool()
						.must(QueryBuilders.term("cid", "1"))
						.should(QueryBuilders.term("cid", "1"))
						.must_not(QueryBuilders.term("cid", "1"))
						.must(QueryBuilders.term("cid2", "2"))
					)
					.must_not(
						BooleanQuery.bool().must(QueryBuilders.term("cid", "1"))
						.should(QueryBuilders.term("cid", "1"))
						.must_not(QueryBuilders.term("cid", "1"))
						.must(QueryBuilders.term("cid2", "2"))
					)
					.should(BooleanQuery.bool().must(QueryBuilders.term("cid", "1")))
				)
			.should(
				BooleanQuery.bool()
					.must(
						BooleanQuery.bool()
						.must(QueryBuilders.term("cid", "1"))
						.should(QueryBuilders.term("cid", "1"))
						.must_not(QueryBuilders.term("cid", "1"))
						.must(QueryBuilders.term("cid2", "2"))
					)
					.must_not(
						BooleanQuery.bool().must(QueryBuilders.term("cid", "1"))
						.should(QueryBuilders.term("cid", "1"))
						.must_not(QueryBuilders.term("cid", "1"))
						.must(QueryBuilders.term("cid2", "2"))
					)
					.should(BooleanQuery.bool().must(QueryBuilders.term("cid", "1")))
				);
		
		System.out.println(filter.toString());
	}
```