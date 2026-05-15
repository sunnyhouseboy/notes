# Java的中文分词器ansj

## 一、引言

Ansj中文分词器，作为一款卓越的开源Java语言工具，它根植于中科院ictclas算法的深厚底蕴，展现出超越众多主流开源分词工具的精准度，如MMseg4j等。Ansj不仅精通于中文分词这一核心技能，更在多个领域展现出其全面性与先进性：它能够精准识别中文姓名，赋予文本处理更深层次的个性化与准确性；支持用户自定义词典，让分词过程更加贴合特定需求与场景；同时，它还集成了关键字提取、自动摘要生成以及关键字标记等高级功能，为文本分析、信息检索等应用提供了强有力的支持。因此，Ansj中文分词器成为了那些对分词效果有着极高要求的各类项目的理想选择，无论是学术研究、商业应用还是个人开发，都能从中受益匪浅。

## 二、使用

### 1、 基本分词-BaseAnalysis

说明：基本分词速度非常快.在macAir上.能到每秒300w字每秒.同时准确率也很高.但是对于新词他的功能十分有限

| 用户自定义词典 | 数字识别 | 人名识别 | 机构名识别 | 新词发现 |
| -------------- | -------- | -------- | ---------- | -------- |
| Χ              | √        | Χ        | Χ          | Χ        |

```java
void demo1() {
        String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
                "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。" +
                "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
        Result analysisedResult = BaseAnalysis.parse(text);
        System.out.println("基本分词: " + analysisedResult);
    }
```

结果：`基本分词: 操作系统/l,（/w,英语/nz,：/w,operating/en, ,system/en,，/w,缩写/n,：/w,os/en,）/w,是/v,一/m,种/q,内置/vn,的/u,程序/n,，/w,用来/v,协作/vn,计算机/n,的/u,各种/r,硬件/n,，/w,以/p,与/p,用户/n,进行/v,交互/v,。/w,常见/a,有/v,windows/en,，/w,macos/en, ,和/c,开源/v,的/u, ,linux/en,。/w,根据/p,运行/vn,的/u,环境/n,，/w,操作系统/l,可以/v,分为/v,桌面/n,操作系统/l,，/w,手机/n,操作系统/l,，/w,服务器/n,操作系统/l,，/w,嵌入式/nz,操作系统/l,等/u,。/w,操作系统/l,是/v,人/n,与/p,计算机/n,之间/f,的/u,接口/n,，/w,也/d,是/v,计算机/n,的/u,灵魂/n,。/w`

==默认的是每个分词的结果都会带有自身的词性，为了后续方便我会隐藏所有的词性==

### 2、 精准分词-ToAnalysis

说明：它在易用性,稳定性.准确性.以及分词效率上.都取得了一个不错的平衡。

| 用户自定义词典 | 数字识别 | 人名识别 | 机构名识别 | 新词发现 |
| -------------- | -------- | -------- | ---------- | -------- |
| √              | √        | √        | Χ          | Χ        |

```Java
void demo2(){
    String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
            "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。" +
            "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
    String analysisedText = ToAnalysis.parse(text).toStringWithOutNature();
    System.out.println("基本分词: " + analysisedText);
}
```

结果：`基本分词: 操作系统,（,英语,：,operating, ,system,，,缩写,：,os,）,是,一种,内置,的,程序,，,用来,协作,计算机,的,各种,硬件,，,以,与,用户,进行,交互,。,常见,有,windows,，,macos, ,和,开源,的, ,linux,。,根据,运行,的,环境,，,操作系统,可以,分为,桌面,操作系统,，,手机,操作系统,，,服务器,操作系统,，,嵌入式,操作系统,等,。,操作系统,是,人,与,计算机,之间,的,接口,，,也,是,计算机,的,灵魂,。`

### 3、nlp分词-NlpAnalysis

说明：它可以识别出未登录词.但是它也有它的缺点.速度比较慢.稳定性差，比较适用于语法实体名抽取等对文本进行发现分析的工作。

| 用户自定义词典 | 数字识别 | 人名识别 | 机构名识别 | 新词发现 |
| -------------- | -------- | -------- | ---------- | -------- |
| √              | √        | √        | √          | √        |

```java
void demo3(){
        String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
                "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。" +
                "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
NlpAnalysis.parse(text).recognition(stopRecognition).toStringWithOutNature();
        String analysisedText = NlpAnalysis.parse(text).toStringWithOutNature();
        System.out.println("nlp分词: " + analysisedText);
    }
```

结果：`nlp分词: 操作系统,（,英语,：,operating, ,system,，,缩写,：,os,）,是,一种,内置,的,程序,，,用,来,协作,计算机,的,各种,硬件,，,以,与,用户,进行,交互,。,常见,有,windows,，,macos, ,和,开源,的, ,linux,。,根据,运行,的,环境,，,操作系统,可以,分为,桌面,操作系统,，,手机,操作系统,，,服务器,操作系统,，,嵌入式,操作系统,等,。,操作系统,是,人,与,计算机,之间,的,接口,，,也,是,计算机,的,灵魂,。`

### 4、面向索引的分词-IndexAnalysis

| 用户自定义词典 | 数字识别 | 人名识别 | 机构名识别 | 新词发现 |
| -------------- | -------- | -------- | ---------- | -------- |
| √              | √        | √        | Χ          | Χ        |

说明：IndexAnalysis是适合在lucene等文本检索中用到的分词，在分词的过程中在这个过程中，召回率（Recall）和准确率（Precision）是两个关键的性能指标，它们用来评估分词的质量。

* **召回率（Recall）**

  召回率衡量的是分词系统能够正确识别出文本中所有相关词项的能力。换句话说，它关注于系统能够找到多少实际存在于文本中的词项。高召回率意味着分词系统能够尽可能地涵盖文本中的所有相关信息，减少遗漏。

*  **准确率（Precision）**

  准确率衡量的是分词系统识别出的词项中，有多少是真正相关或正确的。换句话说，它关注于系统识别的词项中有多少是“真正”的词项，而不是错误的分割或识别。

```java
void demo4(){
    String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
            "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。" +
            "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
    String analysisedText = IndexAnalysis.parse(text).toStringWithOutNature();
    System.out.println("面向索引的分词: " + analysisedText);
}
```

结果：`面向索引的分词: 操作系统,（,英语,：,operating, ,system,，,缩写,：,os,）,是,一种,内置,的,程序,，,用来,协作,计算机,的,各种,硬件,，,以,与,用户,进行,交互,。,常见,有,windows,，,macos, ,和,开源,的, ,linux,。,根据,运行,的,环境,，,操作系统,可以,分为,桌面,操作系统,，,手机,操作系统,，,服务器,操作系统,，,嵌入式,操作系统,等,。,操作系统,是,人,与,计算机,之间,的,接口,，,也,是,计算机,的,灵魂,。`

## 三、其他工具

### 1、停词器

说明：停词器的用法有很多，可以用来剔除某种词性的词，也可以直接指定剔除词汇，还可以使用正则表达式来大范围剔除词汇等。

#### **剔除标点符号**

```java
void demo11(){
    StopRecognition stopRecognition = new StopRecognition();
    String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
            "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。" +
            "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
    //剔除标点符号(w)
    stopRecognition.insertStopNatures("w");//代表原文中的标点符号
    String analysisedText = ToAnalysis.parse(text).recognition(stopRecognition)
            .toStringWithOutNature();
    System.out.println(analysisedText);
}
```

结果：`操作系统,英语,operating, ,system,缩写,os,是,一种,内置,的,程序,用来,协作,计算机,的,各种,硬件,以,与,用户,进行,交互,常见,有,windows,macos, ,和,开源,的, ,linux,根据,运行,的,环境,操作系统,可以,分为,桌面,操作系统,手机,操作系统,服务器,操作系统,嵌入式,操作系统,等,操作系统,是,人,与,计算机,之间,的,接口,也,是,计算机,的,灵魂`

#### **剔除指定词汇**

```Java
void demo11(){
        StopRecognition stopRecognition = new StopRecognition();
        String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
                "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。" +
                "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
        //剔除标点符号(w)
//        stopRecognition.insertStopNatures("w");
        stopRecognition.insertStopWords("操作系统");
        String analysisedText = ToAnalysis.parse(text).recognition(stopRecognition)
                .toStringWithOutNature();
        System.out.println(analysisedText);
    }
```

结果：`（,英语,：,operating, ,system,，,缩写,：,os,）,是,一种,内置,的,程序,，,用来,协作,计算机,的,各种,硬件,，,以,与,用户,进行,交互,。,常见,有,windows,，,macos, ,和,开源,的, ,linux,。,根据,运行,的,环境,，,可以,分为,桌面,，,手机,，,服务器,，,嵌入式,等,。,是,人,与,计算机,之间,的,接口,，,也,是,计算机,的,灵魂,。`

剩下的几个功能就不一一展示了，大家有兴趣的可以自己试试。

### 2、提取关键字

```Java
void demo13(){//关键字提取
        KeyWordComputer kwc = new KeyWordComputer(3);
        String title = "操作系统";
        String text = "牛奶，西瓜，鸡蛋，肉夹馍，苹果，香蕉，西瓜，苹果，牛奶";
        Collection<Keyword> result = kwc.computeArticleTfidf(title, text);
        System.out.println(result);
    }
```

结果：`[西瓜/12.480472393317095, 牛奶/11.556255494233643, 苹果/9.25656615845639]`

### 3、词典的使用

```Java
void demo22() throws Exception {
    String text = "操作系统（英语：Operating System，缩写：OS）是一种内置的程序，用来协作计算机的各种硬件，以与用户进行交互。常见有Windows，macOS 和开源的 Linux。" +
            "根据运行的环境，操作系统可以分为桌面操作系统，手机操作系统，服务器操作系统，嵌入式操作系统等。 [12]\n" +
            "操作系统是人与计算机之间的接口，也是计算机的灵魂。";
    String dic="手机操作系统\t1\n桌面操作系统\t2\n服务器操作系统\t3\n嵌入式操作系统\t4\n人与计算机\t5\tryjsj\n";
    Forest forest = Library.makeForest(new BufferedReader(new StringReader(dic)));
    Library.insertWord(forest, "中国");//插入新的词
    GetWord result=forest.getWord(text);
    String temp = null;
    while ((temp = result.getFrontWords()) != null)
        System.out.println(temp + "\t" + result.getParam(0) + "\t" + result.getParam(1));
}
```

结果：`桌面操作系统	2	null
		  手机操作系统	1	null
		  服务器操作系统	3	null
		  嵌入式操作系统	4	null
		  人与计算机	    5	ryjsj`

可以看到在创建词典的时候要把每一个词单独放在一行，后面跟的“\t1”，这是代表这个词的索引，当然这个索引可以不用按照顺序命名，然后是“人与计算机\t5\tryjsj\n”其中的“\tryjsj”，这个是相当于把“人与计算机”起了个别名为‘ryjsj’。结果输出的相当于是一个树的节点，一个节点有很多属性，每个属性都要其对应的参数，我这里只输出了其中的两个参数。

参考：**[AnsjSeg使用手册](http://nlpchina.github.io/ansj_seg/)**

