اینم یه تجربه پراکنده دیگه!

من این چند روز بخاطر یه کاری نیاز داشتم یه مساله تئوری گراف رو حل کنم. من معمولا سعی میکنم که توی کارها یه چیز جدید رو یاد بگیرم. به همین خاطر با استفاده از [ipython notebook] یا [jupyter notebook] مساله رو حل کردم. اتفاقا [جادی] هم یه [ویدئوی آموزشی] خوب در موردش ساخته.

## چرا Jupyter Notebook

خب اول از همه میخوام یه چیزایی رو توضیح بدم که به نظر من چرا شاید کسی بخواد از این سیستم‌ها استفاده کنه. مهم‌ترین استفاده‌ای که من براش داشتم اینه که هر جا که به نظرم میخواستم از [matlab] استفاده کنم میتونستم از [jupyter notebook] استفاده کنم. بدین شکل که شما برای خیلی کارهای علمی یه کارهایی رو توی [matlab] پیاده‌سازی میکنی و تست می‌کنی و وقتی لازم شد واقعا در محیط عملیاتی ازش استفاده کنی اون‌ها رو در محیط عملیاتی دوباره پیاده‌سازی می‌کنی.

خب اولین زبانی که [jupyter notebook] پشتیبانی میکرده [python] بوده که مثل زبان [matlab] ساده بوده و بخاطر پکیج‌های عملی که هر دو زبان دارن پیاده‌سازی کارهای علمی به شدت ساده می‌شه. 

دوم اینکه هر دو از مفهوم به نام متغیرهای مشترک بین همه برنامه‌های مختلف پشتیبانی می‌کنن که باعث میشه شما یه کار پر هزینه رو یه بار انجام بدی و نتیجه رو داشته باشی و مراحل بعدی رو براساس اون و بدون نیاز به اجرای از اول اون بخش پر هزینه انجام بدی

سوم اینکه هر دو ابزارهای بسیار خوب و قوی برای کشیدن نمودارهای علمی دارن که باعث میشه گزارش ساختن با اونها راحت باشه.

چهارم اینکه در [jupyter notebook] شما می‌تونید همزمان که کد می‌نویسید گزارش هم بنویسید. یعنی بلوک‌هایی داریم که توش میشه با استفاده از [markdown] متن هم بنویسید که در نهایت گزارش کاری که دارید انجام می‌دید هم آماده باشه. لازم نیست تکرار کنم که [markdown] رو من خیلی دوست دارم([1] و [2] و [3])

## یه مثال ساده

حالا کار من این بود که بتونم یه [گراف جهت‌دار بدون دور] بسازم و بتونم اون رو بکشم. خب اول از هم نحوه ساختن اون. کلا در ریاضی اثبات میشه که اگه بخواید [گراف جهت‌دار بدون دور] بسازید تنها چیزی که نیاز دارید اینه که توی ماتریس مجاورت اون گراف تنها درایه‌های زیر قطر اصلی ۱ باشن. این تضمین می‌کنه که گراف تولید شده [گراف جهت‌دار بدون دور] باشه.

اول از همه باید نیازمندی ها رو وارد کرد

	%matplotlib inline

	import numpy as np
	import random
	import networkx as nx
	import matplotlib.pyplot as plt
	from nxpd import draw
	from nxpd import nxpdParams
	import copy

	nxpdParams['show'] = 'ipynb'

بعد نوبت به کد ساختن DAG میرسه که کد این کار اینه


	def generateDAG(nodeNo, edgeProb):
	    adj = np.zeros((nodeNo, nodeNo))
	    G=nx.DiGraph()
	    deps = dict()
	    nodeLables = list(range(nodeNo))
	    addedLabels = list()
	    
	    for i in range(nodeNo):
		lIdx = random.randrange(len(nodeLables))
		lable = nodeLables[lIdx]
		addedLabels.append(lable)
		nodeLables.remove(lable)
		
		G.add_node(str(addedLabels[i]))
		deps[str(addedLabels[i])] = set()
		for j in range(i):
		    rnd = random.random()
		    if  rnd < edgeProb and i != j:
		        G.add_edge(str(addedLabels[j]), str(addedLabels[i]))
		        deps[str(addedLabels[i])].add(str(addedLabels[j]))
		        adj[i,j]= 1
	    return (adj, G, deps)

بعدش هم میشه نمایش دادنش که به سادگی میشه این


	nodeCount = 10
	dependencyProbability= 0.7
	dag, G, deps = generateDAG(nodeCount,dependencyProbability)
	draw(G)

نتیجه کار هم توی [github] قرار گرفته و از [اینجا] قابل مشاهده است.
همین!

[ipython notebook]:https://en.wikipedia.org/wiki/IPython#Project_Jupyter
[jupyter notebook]:https://en.wikipedia.org/wiki/IPython#Project_Jupyter
[matlab]:https://en.wikipedia.org/wiki/MATLAB
[python]:https://en.wikipedia.org/wiki/Python_(programming_language)
[markdown]:https://en.wikipedia.org/wiki/Markdown
[github]:https://github.com/yazdan/myNotebooks
[1]:http://blog.abyz.ir/1394/03/markdown-my-doc-generation-format/
[2]:http://blog.abyz.ir/1394/04/%d9%85%d8%b4%da%a9%d9%84-%d8%aa%d9%88%d9%84%db%8c%d8%af-%d9%85%d8%ad%d8%aa%d9%88%d8%a7-%d8%b1%d9%88%db%8c-%d9%85%d9%88%d8%a8%d8%a7%db%8c%d9%84-%d9%88-%d8%aa%d8%a8%d9%84%d8%aa/
[3]:http://blog.abyz.ir/1393/10/markdown-latex-html/
[جادی]:https://jadi.net
[گراف جهت‌دار بدون دور]:https://en.wikipedia.org/wiki/Directed_acyclic_graph
[ویدئوی آموزشی]:http://jadi.net/2015/08/jaditv-007-ipython-notebook-vcf/
[اینجا]:https://nbviewer.jupyter.org/github/yazdan/myNotebooks/blob/master/DagTutorial.ipynb
