import os,random,sys,time
import parameters
#from browserlib.parser import urlprase
from selenium import webdriver
from bs4 import BeautifulSoup
from time import sleep
import selector
import urllib3
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.action_chains import ActionChains
browser= webdriver.Chrome('driver_win32/chromedriver.exe') # after runing this line new window tab will be open
browser.get('https://www.linkedin.com/uas/login')
file= open('config.txt')
line= file.readlines()
username=line[0]
password=line[1]
elementID = browser.find_element_by_id('username')
elementID.send_keys(username)
elementID= browser.find_element_by_id('password')
elementID.send_keys(password)

df1=[]
df2=[]
df3=[]
df4=[]
df5=[]

browser.implicitly_wait(1)

log_in_button = browser.find_element_by_class_name("from__button--floating")


log_in_button.click()
for i in range(10):
    browser.get('https:www.google.com')
    browser.implicitly_wait(1)

    search_query = browser.find_element_by_name('q')
    search_query.send_keys('site:linkedin.com/in/ AND "python Developer" AND "Web developer"' + 'page' + '' + str(i))
    browser.implicitly_wait(1)


    search_query.send_keys(Keys.RETURN)
    browser.implicitly_wait(1)

    linkendin_urls=browser.find_elements_by_class_name('iUh30')
    linkendin_urls= [url.text for url in linkendin_urls]
    ##linkendin_urls=[i.split(" ",2)[2] for i in linkendin_urls]
    print(linkendin_urls)
    browser.implicitly_wait(1)

    browser.get('https://www.linkedin.com/in/gajanan-gadekar-10a4b9112/')

    src = browser.page_source()

    browser.implicitly_wait(1)

    for linkedin_url in linkendin_urls:
        browser.get('https://www.linkedin.com/in/'+ linkedin_url)

        browser.implicitly_wait(2)


        sel= selector(text=browser.page_source)


        print('\n')

        name= sel.xpath('//[starts-with(@class,"inline t-24 t-black t-normal break-words")]/text()').extract_first()
        if name:
            name=name.strip()
            print('Name:' +name)
            df1.append(name)
        job_title=sel.xpath('//h2/text()').extract_first()
        if job_title:
            job_title=job_title.strip()
            print('Job Title:'+job_title)
            df2.append(job_title)
        location=sel.xpath('//[starts-with(@class,"inline t-16 t-black t-normal inline-block")]/text()').extract_first()
        if location:
            location=location.strip()
            print('Location:'+location)
            df3.append(location)
        employer=sel.xpath('//*[starts-with(@class,"text-align-left m12 t-14 t-black t-bold full-width it-line)]/text()').extract_first()
        if employer:
            employer=employer.strip()
            print('company:' +employer)
            df4.append(employer)

        education= sel.xpath('//*[starts-with(@id,"ember96")]/text()').extract_first()
        if education:
            education=education.strip()
            print('College:'+education)
            df5.append(education)
        print('URL:' +'https://www.linkedin.com/in/' + linkedin_url)
        print('\n')

        linkedin_url=browser.current_url
import pandas as pd

linkedin= pd.DataFrame([df1,df2,df3,df4,df5])
linkedin.to_csv('auto_link.csv')





