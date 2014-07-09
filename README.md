solr-php
========

The first set of PHP Solr libraries that were available for SOLR

## SolrUpdate Instructions


This class performs an update on an existing Solr repository
It uses the handy ADODB database library, but you can substitute your own if you prefer.
ADODB makes dealing with SQL much nicer than the php mysql_ calls and handy if you switch databases.
http://adodb.sourceforge.net/


## SQL TABLE Notice:

Inside your table that stores the primary key for your data or each record, create a tinyint(1) (or enum) flag 
called "index_flag".  Ex:
```sql
ALTER TABLE `stories` ADD `index_flag` TINYINT( 1 ) NOT NULL ;
```
This will allow the update process to continue where it left off in case there is an error.


## Example usage:


```php
<?php

require_once("config.php"); // config file
require_once(PHYSICALDIR."/ops/lib/common.php");
$DB=createADODB();
$solr = new SolrUpdate;
$solr->updateIndex();
? >


// From within a PHP function
// This example will perform batch updates

$solr = new SolrUpdate();

$containerarray = array();

$array = array();
$array['story_id'] = $story_id;
$array['group_id'] = $group_id;
$array['lucene_date'] = $lucene_date;
$array['title'] = $title;

$containerarray[]=$array;
$array = array();
$array['story_id'] = $story_id;
$array['group_id'] = $group_id;
$array['lucene_date'] = $lucene_date;
$array['title'] = $title;

$containerarray[]=$array;

$solr->addIndex($containerarray);

```

## SolrQuery Instructions

```php
                $query = new SolrQuery;
        
                $query->language_id = $this->language_id;
                $query->lowerdate = $day_3neg;
                $query->upperdate = $day_3pos;
                $query->limit = 10;
                $query->group_id = 1;

                $results = $query->runQuery($titlekeywords);
                print_r($results);
```