# Source-code Summarization
This repository contais all investigation data about source-code summarization techniques explored so far.

## Funcom

LeClair, A., Jiang, S., McMillan, C., "A Neural Model for Generating Natural Language Summaries of Program Subroutines", in Proc. of the 41st ACE/IEEE International Conference on Software Engineering (ICSE'19), Montreal, QC, Canada, May 25-31, 2019.
[Link to publication](https://arxiv.org/abs/1902.01954)

### Original repo
[Link to original repo](https://github.com/mcmillco/funcom)

### Source-code modifications
To be able to run training and predicting scripts on [Google Colab](https://colab.research.google.com), I have migrated the code from tensorflow 1.x to tensonflow 2.x. Apart from that, some properties were also not up to date with the provided data (Ex. 'dttrain' should be 'dtrain').

### Jupyter Notebook

[funcom.ipynb](https://colab.research.google.com/drive/18PP0Tz1ZGBA36ymXQ97opweQPqp5ul4P#scrollTo=D8hetAatfQYc)

```python
# Train data (just 1 epoch due to resources limitation)

%run '/content/drive/MyDrive/Doutorado/funcom/train.py' --model-type=attendgru --epochs=1 --gpu=0
```
```python
# Predict using generated model (.h5 file)

%run '/content/drive/MyDrive/Doutorado/funcom/predict.py' '/content/drive/MyDrive/Doutorado/funcom_scratch/data/outdir/models/attendgru_E01_1662135594.h5' --gpu=0
```
### Results

#### Example 1: 6314323
Prediction: `recalculate column and row count`

Reference:  `recalculates the column and row count considering all data`

Source-code:
```java
/**
  * recalculates the column and row count considering all data.
  * To be used after a delete
  */
private void recalculateColumnAndRowCount() {
    columnCount = 0;
    rowCount = 0;
    for (PresentedData data : mapDataById.values()) 
        changeColumnAndRowCountForData(data);
}
```

Source-code (tokenized):
```java
private void recalculate column and row count column count 0 row count 0 for presented data data map data by id values change column and row count for data data
```

#### Example 2: 8868643
Prediction: `returns true if the given field is available`

Reference: `checks if index is available`

Source-code:
```java
/**
  * Checks if index is available
  * @param fullTextSession
  * @return
  * @throws ParseException
  */
public boolean indexAvailable(Class clazz, String fieldName) throws ParseException {
    Session session = sessionFactory.openSession();
    FullTextSession fullTextSession = Search.getFullTextSession(session);
    org.apache.lucene.queryParser.QueryParser parser = new QueryParser(
        fieldName, fullTextSession.getSearchFactory().getAnalyzer(clazz));
    org.apache.lucene.search.Query luceneQuery = parser.parse("*:*");
    Query query = fullTextSession.createFullTextQuery(luceneQuery, clazz);
    query.setMaxResults(1);
    List results = query.list();
    boolean indexAvailable = results.size()>0;
    fullTextSession.close();
    return indexAvailable;
}
```

Source-code (tokenized):
```java
public boolean index available class clazz string field name throws parse exception session session session factory open session full text session full text session search get full text session session org apache lucene query parser query parser parser new query parser field name full text session get search factory get analyzer clazz org apache lucene search query lucene query parser parse query query full text session create full text query lucene query clazz query set max results 1 list results query list boolean index available results size 0 full text session close return index available
```

#### Example 3: 4512280 / 4520308
Prediction: `invoked when a mouse has been clicked`

Reference: `activate and notify the logic observer`

Source-code:
```java
/**
  * Activate and notify the logic observer
  * that the space was clicked if the space
  * is setable.
  */
public void mouseClicked(MouseEvent e) {
    if (this.setable) {
        this.notifyObserver(e);
    }
}
```

Source-code (tokenized):
```java
public void mouse clicked mouse event e if this setable this notify observer e
```

#### Example 4: 22622498
Prediction: `sets the debug flag`

Reference: `sets the debug attribute of the record validation filter object`

Source-code:
```java
/**
  * Sets the debug attribute of the RecordValidationFilter object
  *
  * @param db The new debug value
  */
protected void setDebug(boolean db) {
    debug = db;
}
```

Source-code (tokenized):
```java
protected void set debug boolean db debug db
```

#### Example 5: 18925380
Prediction: `adds a new configuration to the file`

Reference: `adds a log4j configuration to the list of predefined configs`

Source-code:
```java
/**
  * adds a log4j configuration to the list of predefined configs
  * @param resourceName name of the resource, ".properties" will be appended. 
  * Example: "/my/package/log4jdebug"
  * @param label will be presented to the user
  */
public void addConfig(String resourceName, String label) throws IOException {
    // copy file if not already there
    String name = resourceName;
    int pos = name.lastIndexOf('/');
    if (pos >= 0)
        name = name.substring(pos + 1);
    File file = new File(logDir, name + ".properties");
    if (!file.exists())
        copyRes(resourceName + ".properties", file);
    // add to config
    configs.put(name, file);
    labels.put(name, label);
}
```

Source-code (tokenized):
```java
public void add config string resource name string label throws ioexception copy file if not already there string name resource name int pos name last index of if pos 0 name name substring pos 1 file file new file log dir name properties if file exists copy res resource name properties file add to config configs put name file labels put name label
```
