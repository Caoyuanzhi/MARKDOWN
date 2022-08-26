
### c++11正則
```c++
void run5() {
    string s = "aa  bb cc   dd";
    regex pattern("\\s+");
    vector<string> vec(sregex_token_iterator(s.begin(), s.end(), pattern, -1), sregex_token_iterator());
    for(auto inner: vec) {
        cout<<inner<<endl;
    }
}
```

### find()
```c++
void run() {
    string s = "aa bb cc dd";
    const string delim = " ";
    int nPos = 0;
    vector<string> vec;
    nPos = s.find(delim.c_str());
    while(-1 != nPos) {
        string temp = s.substr(0, nPos);
        vec.push_back(temp);
        s = s.substr(nPos+1);
        nPos = s.find(delim.c_str());
    }
    vec.push_back(s);
    
    for(string ele: vec) {
        cout<<ele<<" ";
    }
}
```

### other
```c++
vector<string> split(const string& str, const string& delim) {  
	vector<string> res;  
	if("" == str) return res;  
	//先将要切割的字符串从string类型转换为char*类型  
	char * strs = new char[str.length() + 1] ; //不要忘了  
	strcpy(strs, str.c_str());   
 
	char * d = new char[delim.length() + 1];  
	strcpy(d, delim.c_str());  
 
	char *p = strtok(strs, d);  
	while(p) {  
		string s = p; //分割得到的字符串转换为string类型  
		res.push_back(s); //存入结果数组  
		p = strtok(NULL, d);  
	}  
 
	return res;  
} 
```

### stackoverflow
https://zhuanlan.zhihu.com/p/56163976
```c++
void split(const string& s, vector<string>& tokens, const char& delim = ' ') {
    tokens.clear();
    size_t lastPos = s.find_first_not_of(delim, 0);
    size_t pos = s.find(delim, lastPos);
    while (lastPos != string::npos) {
        tokens.emplace_back(s.substr(lastPos, pos - lastPos));
        lastPos = s.find_first_not_of(delim, pos);
        pos = s.find(delim, lastPos);
    }
}
```


https://stackoverflow.com/questions/26328793/how-to-split-string-with-delimiter-using-c
```c++
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;

static string& strip(string& s, const string& chars = " ")
{
        s.erase(0, s.find_first_not_of(chars.c_str()));
        s.erase(s.find_last_not_of(chars.c_str()) + 1);
        return s;
}

static void split(const string& s, vector<string>& tokens, const string& delimiters = " ")
{
        string::size_type lastPos = s.find_first_not_of(delimiters, 0);
        string::size_type pos = s.find_first_of(delimiters, lastPos);
        while (string::npos != pos || string::npos != lastPos) {
                tokens.push_back(s.substr(lastPos, pos - lastPos));
                lastPos = s.find_first_not_of(delimiters, pos);
                pos = s.find_first_of(delimiters, lastPos);
        }
}

static void parse(string& s, map<string,string>& items)
{
        vector<string> elements;
        s.erase(0, s.find_first_not_of(" {"));
        s.erase(s.find_last_not_of("} ") + 1);
        split(s, elements, ",");
        for (vector<string>::iterator iter=elements.begin(); iter != elements.end(); iter++) {
                vector<string> kv;
                split(*iter, kv, ":");
                if (kv.size() != 2) continue;
                items[strip(kv[0], " \"")] = strip(kv[1], " \"");
        }
}

int main()
{
        string data = "  {  \"key1\"  :  \"data1\"  ,  \"key2\"  :  \"data2\"    }  ";
        map<string,string> items;
        parse(data, items);

        for (map<string,string>::iterator iter=items.begin(); iter != items.end(); iter++) {
                cout << "key=" << (*iter).first << ",value=" << (*iter).second << endl;
        }
}
```

