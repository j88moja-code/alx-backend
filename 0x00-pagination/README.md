## 0x00-pagination

`mandatory_tasks`

* [0-simple_helper_function.py](https://github.com/j88moja-code/alx-backend/blob/main/0x00-pagination/0-simple_helper_function.py) - a function named `index_range` that takes two integer arguments page and `page_size.`
* [1-simple_pagination.py](https://github.com/j88moja-code/alx-backend/blob/main/0x00-pagination/1-simple_pagination.py) - copy `index_range` from the previous task and the following class into your code
```
import csv
import math
from typing import List


class Server:
    """Server class to paginate a database of popular baby names.
    """
    DATA_FILE = "Popular_Baby_Names.csv"

    def __init__(self):
        self.__dataset = None

    def dataset(self) -> List[List]:
        """Cached dataset
        """
        if self.__dataset is None:
            with open(self.DATA_FILE) as f:
                reader = csv.reader(f)
                dataset = [row for row in reader]
            self.__dataset = dataset[1:]

        return self.__dataset

    def get_page(self, page: int = 1, page_size: int = 10) -> List[List]:
            pass
```
* Implement a method named `get_page` that takes two integer arguments `page` with default value 1 and `page_size` with default value 10.
* [2-hypermedia_pagination.py](https://github.com/j88moja-code/alx-backend/blob/main/0x00-pagination/2-hypermedia_pagination.py) - Replicate code from the previous task.

	* Implement a `get_hyper` method that takes the same arguments (and defaults) as `get_page` and returns a dictionary containing the following key-value pairs:

		* `page_size`: the length of the returned dataset page
		* `page`: the current page number
		* `data`: the dataset page (equivalent to return from previous task)
		* `next_page`: number of the next page, `None` if no next page
		* `prev_page`: number of the previous page, `None` if no previous page
		* `total_pages`: the total number of pages in the dataset as an integer
	* Make sure to reuse `get_page` in your implementation.
* [3-hypermedia_del_pagination.py](https://github.com/j88moja-code/alx-backend/blob/main/0x00-pagination/3-hypermedia_del_pagination.py) - The goal here is that if between two queries, certain rows are removed from the dataset, the user does not miss items from dataset when changing page.

Start `3-hypermedia_del_pagination.py` with this code:
```
#!/usr/bin/env python3
"""
Deletion-resilient hypermedia pagination
"""

import csv
import math
from typing import List


class Server:
    """Server class to paginate a database of popular baby names.
    """
    DATA_FILE = "Popular_Baby_Names.csv"

    def __init__(self):
        self.__dataset = None
        self.__indexed_dataset = None

    def dataset(self) -> List[List]:
        """Cached dataset
        """
        if self.__dataset is None:
            with open(self.DATA_FILE) as f:
                reader = csv.reader(f)
                dataset = [row for row in reader]
            self.__dataset = dataset[1:]

        return self.__dataset

    def indexed_dataset(self) -> Dict[int, List]:
        """Dataset indexed by sorting position, starting at 0
        """
        if self.__indexed_dataset is None:
            dataset = self.dataset()
            truncated_dataset = dataset[:1000]
            self.__indexed_dataset = {
                i: dataset[i] for i in range(len(dataset))
            }
        return self.__indexed_dataset

    def get_hyper_index(self, index: int = None, page_size: int = 10) -> Dict:
            pass
```
Implement a `get_hyper_index` method with two integer arguments: `index` with a `None` default value and `page_size` with default value of 10.
