---
title: "3. Algorithm"
categories: Third blog
tags: blog
---

코드: 
```C++ 
include <iostream>
using namespace std;

int main()
{
	int sugar, bag_5, bag_3, result = 0;
	cin >> sugar;

	for (bag_3 = 0; 3*bag_3 <= sugar; bag_3++)
	{
		for (bag_5 = 0; 5*bag_5 <= sugar - 3*bag_3; bag_5++)
		{

			if (sugar < 3 * bag_3 + 5 * bag_5)
				break;
			if (sugar == 3 * bag_3 + 5 * bag_5)
			{
				result = bag_3 + bag_5;
				break;
			}
		}
		if (result > 0)
			break;
	}
		
	if (result == 0)
		result = -1;

	cout << result; 
}
```

