#personal #DSA

# Unordered Maps
1. `unordered_map<int, int>mp;`
2. `mp.find(elem)` returns an iterator of the first occurrence of `elem` and returns `mp.end()` if not found
3. Access `auto it = mp.find(elem)` as `it->first` and `it->second`
4. Keys are stored in a random order

# sets
1. `std::set<int> st{};`
2. `st.insert(elem);`
3. `vector<int> set_vector(st.begin(), st.end());`
4. `st.begin()` and `st.end()`
5. Convert set to vector by `vector<int> set_vec(st.begin(), st.end())`
6. The keys, ie, the element itself, are stored in a sorted order

# maps
1. `std::map<int, int> mp{}`
2. 
 ```
 for(auto &it: mp)
	 cout << mp.first
 ```
 Here, `for(auto it: mp)` can also be used. However, the value will be copied instead of being reference and hence, will be less efficient
 3. `mp.first` is the key and `mp.second` is the value
 4. The elements are of type `std::pair<int, int>`
 5. The keys are stored in ascending order

# vectors
1. `vec.end()` returns an iterator pointing to the (theoretical)element that would follow the current last element in the array
2. `*(vec.end() - 1)` for the last element
3. `vec.begin()` returns an iterator to the first element
4. `reverse(vec.begin() + n, vec.end() - m)` reverses the elements in the range [n, m)
5. `vec.empty()` returns 1 if the vector is empty and 0 otherwise
6. `for(auto it{mp.begin()}; it != mp.end(); it++)` for iterator based iteration
7. `next(it)` is a pointer to the next iterator and `prev(it)` to the previous iterator of `it`
8. `fill(v.begin(), v.end(), val);` fills the range with value `val`