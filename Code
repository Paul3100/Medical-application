
from datetime import datetime
import pickle
import sqlite3
from tkinter.ttk import Combobox

from tkcalendar import *
#### my library
import interact
import order
############
import requests
import tkinter as Tk
import sys
import tkinter.scrolledtext as sc
from selenium import webdriver
from selenium.common.exceptions import TimeoutException
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
import bs4 as bs
from bs4 import BeautifulSoup
from tkinter import ttk
import threading
from tkinter import messagebox
from tkinter import *
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import bs4 as bs
import tkinter
from bs4 import BeautifulSoup
import urllib.request
from multiprocessing import Queue
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import time
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import *
from multiprocessing import Process
import multiprocessing
from tkinter import messagebox
import hashlib
import smtplib
# email
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
import os

import httplib2
import os
import base64
from apiclient import discovery
from oauth2client import client
from oauth2client import tools
from oauth2client.file import Storage
from auth import auth
import re
import selenium.webdriver.common.keys
from selenium.webdriver.common.keys import Keys
import quickstart
import calendar_quickstart
import ast
from ast import literal_eval
import json
from selenium.webdriver.chrome.options import Options
class sign_up():
    def __init__(self, canvas):
        self.canvas = canvas
        # creating sign up frame
        self.register = Frame(self.canvas, bg="gray")
        self.register.place(relwidth=800, relheight=500, rely=0.05)
        self.title = Label(self.register, text="Account Creation", relief="sunken", bg="cyan", padx=6, pady=6)
        self.title.place(y=60, height=34, width=323, x=216)
        # entry boxes
        self.name = Entry(self.register, bd=4)
        self.name.place(height=24, width=175, x=360, y=120)
        self.address = Entry(self.register, bd=4)
        self.address.place(height=24, width=175, x=360, y=180)
        self.password = Entry(self.register, bd=4, show="*")
        self.password.place(height=24, width=175, x=360, y=240)
        # labels
        self.name_label = Label(self.register, text="Name:", bd=4, padx=5, bg="gray")
        self.name_label.place(height=24, width=175, x=150, y=120)
        self.address_label = Label(self.register, text="Email address:", bd=4, padx=5, bg="gray")
        self.address_label.place(height=24, width=150, x=183, y=180)
        self.password_label = Label(self.register, text="Password:", bd=4, padx=5, bg="gray")
        self.password_label.place(height=24, width=150, x=173, y=240)
        # button - checks if user is already registered
        self.put_into_system = Button(self.register, text="Sign up", padx=6, pady=6, cursor="tcross",
                                      command=lambda: self.checker(self.name.get(), self.password.get(),
                                                                   self.address.get()))
        self.put_into_system.place(height=27, width=150, x=553, y=380)

    def checker(self, name, password, address):

        self.name_ = name
        self.password_ = hashlib.sha256(password.encode()).hexdigest()
        self.address_ = address
        #

        # regular expression
        # for validating an Email
        self.regex = '^[a-z0-9]+[\._]?[a-z0-9]+[@]\w+[.]\w{2,3}$'
        self.regex_ = "^[a-z0-9]+[\._]?[a-z0-9]+[@]\w+[.]\w+$"
        self.regexing = '^[A-Z0-9]+[\._]?[a-z0-9]+[@]\w+[.]\w{2,3}$'
        if (re.search(self.regex, self.address_)) or (re.search(self.regex_, self.address_)) or (
                re.search(self.regexing, self.address_)):
            pass
        else:
            self.restart = sign_up(self.canvas)
            return (messagebox.showinfo("Incorrect standard",
                                        "Check all fields have been completed to an appropriate standard"))

        # global will be used to fetch id of user so bookmark can be placed in the correct row
        global email_of_user
        email_of_user = address

        self.conn = sqlite3.connect('linked tables_two', timeout=10)
        self.c = self.conn.cursor()

        self.Details = "CREATE TABLE IF NOT EXISTS Details(id INTEGER PRIMARY KEY,email_address VARCHAR(50) ,password VARCHAR(50))"
        self.c.execute(self.Details)
        self.Activities = "CREATE TABLE IF NOT EXISTS Activities(id INTEGER PRIMARY KEY ,bookmarks ,Dates VARCHAR(8000),name VARCHAR(50),Gmail VARCHAR(8000),FOREIGN KEY(id) REFERENCES Details(id) ON DELETE CASCADE)"
        self.c.execute(self.Activities)

        # selecting email address - to check if account already exists
        self.c.execute("SELECT email_address FROM Details")
        # boolean value if False then details will not be put into sql database
        self.go_ahead = True
        for i in self.c:
            # i is tuple so needs to be converted into a list, because there is only one item in the list you take value[0]
            if self.address_ == list(i)[0]:
                self.name.delete(0, END)
                self.address.delete(0, END)
                self.password.delete(0, END)
                self.go_ahead = False
                messagebox.showinfo("Attempt to Sign up", "This account already exists, try Logging in")
                login(self.canvas)
                break

        if self.go_ahead == True:
            # self.c.execute("INSERT INTO Users(name) VALUES (?);",(self.name_,))
            self.c.execute("INSERT INTO Details(email_address, password) VALUES (?,?);",
                           (self.address_, self.password_,))
            self.c.execute("INSERT INTO Activities(name) VALUES (?);",
                           (self.name_,))

            self.conn.commit()
            self.name.delete(0, END)
            self.address.delete(0, END)
            self.password.delete(0, END)
            messagebox.showinfo("Attempt to Sign up", "Your account has been successfully created")
            global authenticated
            authenticated = True
            self.final = authorisation_final_step(self.canvas, self.address_)
            searching_frame.tkraise()
        self.conn.close()
class authorisation_final_step():
    def __init__(self, canvas, address):
        self.canvas = canvas
        self.address_ = address
        self.conn = sqlite3.connect('linked tables_two', timeout=10)
        self.c = self.conn.cursor()
        # This is used to get ID which will be used throughout the program to save data uniquely to the user
        self.get = self.c.execute("SELECT id FROM Details WHERE email_address =(?)", (self.address_,))
        self.get = self.get.fetchall()
        global ID
        ID = list(self.get)[0][0]
        # Needs to be amended to particular ID -- NEED GLOBALISED ID IN BOTH LOGIN AND SIGN UP
        global bookmarks
        global Dates
        global GMAIL

        # adding all of te bookmarks into one list
        self.bookmarks = self.c.execute("SELECT bookmarks FROM Activities where ID = (?)", (ID,))
        self.bookmarks = self.bookmarks.fetchall()
        if type(self.bookmarks[0][
                    0]) == str:  # assuming the list has already had a condition added to it and has therefore been converted into json, we need to fetch that specifc value and decode it
            bookmarks = json.loads(self.bookmarks[0][0])
        else:
            bookmarks = []

        # adding all of the dates into one list
        self.dates = self.c.execute("SELECT Dates FROM Activities where ID = (?)", (ID,))
        self.dates = self.dates.fetchall()
        Dates = self.dates

        # adding all of the emails into one list
        self.gmail = self.c.execute("SELECT Gmail FROM Activities where ID = (?)", (ID,))
        self.gmail = self.gmail.fetchall()
        GMAIL = self.gmail

        self.count = 0
        self.conditions = []
        # Fetches bookmarks and adds them into homepage's menu button
        if authenticated == True:
            for i in range(0, len(bookmarks)):
                self.x = bookmarks[i]
                self.conn.close()
                menu.add_command(label=self.x, command=lambda: medical_text(canvas, self.x))

        self.conn.close()
class login():
    def __init__(self, canvas):
        self.canvas = canvas
        # creating sign up frame
        self.log = Frame(self.canvas, bg="gray")
        self.log.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)
        self.title = Label(self.log, text="Log in", relief="sunken", bg="cyan", padx=6, pady=6)
        self.title.place(y=60, height=34, width=323, x=216)
        # entry boxes
        self.address = Entry(self.log, bd=4)
        self.address.place(height=24, width=175, x=360, y=180)
        self.password = Entry(self.log, bd=4, show="*")
        self.password.place(height=24, width=175, x=360, y=240)
        # labels
        self.address_label = Label(self.log, text="Email address:", bd=4, padx=5, bg="gray")
        self.address_label.place(height=24, width=150, x=183, y=180)
        self.password_label = Label(self.log, text="Password:", bd=4, padx=5, bg="gray")
        self.password_label.place(height=24, width=150, x=173, y=240)
        # log in button
        self.put_into_system = Button(self.log, text="Log in", padx=6, pady=6, cursor="tcross",
                                      command=lambda: self.checker(self.password.get(), self.address.get()))
        self.put_into_system.place(height=27, width=150, x=553, y=380)

    def checker(self, password, email):
        self.password_ = password
        self.address_ = email
        global email_of_user
        email_of_user = email
        try:
            self.conn = sqlite3.connect('linked tables_two', timeout=10)
            self.c = self.conn.cursor()
            # selecting email address - to check if account already exists
            self.c.execute("SELECT password FROM Details where email_address = (?)", (self.address_,))
            self.password_fetched = self.c.fetchmany()[0][
                0]  # Throws IndexError: if email does not exist, catch error. Create test data for documentation
            if self.password_fetched == hashlib.sha256(self.password_.encode()).hexdigest():
                messagebox.showinfo("Log in", "You have been Logged in")
                global authenticated
                authenticated = True
                self.final = authorisation_final_step(self.canvas, self.address_)
                searching_frame.tkraise()
            else:
                messagebox.showinfo("Log in", "Incorrect details")
        except:
            messagebox.showinfo("Log in", "Incorrect details")

        self.conn.close()
class medical_articles():
    def __init__(self, canvas):
        self.canvas = canvas
        self.url_number = 1
        self.page_number = 1
        # creating sign up frame
        self.article = Frame(self.canvas, bg="gray")
        self.article.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)
        self.title = Label(self.article, text="News", relief="sunken", bg="cyan", padx=6, pady=6)
        self.title.place(y=60, height=34, width=323, x=216)
        self.nhs_articles = requests.get('https://www.nhs.uk/news/')
        self.health = self.nhs_articles.content
        self.health_two = BeautifulSoup(self.health, 'html.parser')
        self.links = self.health_two.find_all(class_="nhsuk-u-margin-bottom-6")
        self.lis = self.links[0].find_all('li')
        self.categories = []
        self.a = True
        self.count = 0
        self.names_categories = []
        try:
            while self.a == True:
                self.first = self.lis[self.count]
                self.liftedli = self.first.a
                self.names_categories.append(self.liftedli["href"])
                self.url = "https://www.nhs.uk"
                self.url += self.liftedli["href"]
                self.categories.append(self.url)
                self.count += 1
        except:
            self.options = Listbox(self.article, width=64)
            count = 1
            for item in self.names_categories:
                self.categories_replacement = item
                self.categories_replacement = self.categories_replacement.replace("/", " ")
                self.categories_replacement = self.categories_replacement.replace("news", " ")
                self.categories_replacement = self.categories_replacement.replace("-", " ")
                self.categories_replacement = self.categories_replacement[3].upper() + self.categories_replacement[4:]
                self.options.insert(count, self.categories_replacement)
                count += 1

            self.options.place(x=100, y=180, height=213)

            self.search = Button(self.article, text="Search", width=10, relief=RAISED, cursor="tcross",
                                 command=self.article_second_frame)
            self.search.place(x=580, y=368)
            self.search_label = Label(self.article, width=55, text="Search for a category")
            self.search_label.place(x=100, y=150)

    def article_second_frame(self):
        try:
            # not scraping category but only main page
            self.selection = self.options.curselection()
            self.category_link = self.categories[self.selection[0]]  # This is the link for the user's chosen category
        except IndexError:
            messagebox.showinfo("Warning",
                                "Please select a category")
            return (None)

        # opening the url to scrape links in that category
        self.category_link = self.category_link + "?page=" + str(self.url_number)
        self.category_articles = requests.get(self.category_link)
        self.category = self.category_articles.content
        self.scrape_article = BeautifulSoup(self.category, 'html.parser')

        self.max = self.scrape_article.find(class_="nhsuk-pagination__page")
        self.max = self.max.text
        # last two items of text containing current page and what its out of - fetches last two values = the max page
        self.max = self.max[len(self.max) - 2:len(self.max)]

        self.fetch()

    def fetch(self):
        self.articles = Frame(self.canvas, bg="gray")
        self.articles.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)
        self.mylist = Listbox(self.articles, width=132, bg="gray")
        self.mylist.place(x=0, y=30, height=420)

        def home():
            # Ensures page restarts at one, instead of the page number left off from previously selected bookmark
            self.url_number = 1
            self.page_number = 1
            #
            self.article.tkraise()

        self.toolbar = Frame(self.articles)
        self.Back = Button(self.toolbar, text="⇦", command=home)
        self.Back.pack(side=LEFT)
        self.toolbar.pack(side=TOP, fill=X)

        self.links = self.scrape_article.find_all(class_="nhsuk-list nhsuk-list--border")
        self.lis = self.links[0].find_all('li')
        #####################################################
        self.maximum_page = self.scrape_article.find_all(class_="nhsuk-pagination__page")
        #####################################################

        self.removing_dates = self.scrape_article.find_all(
            class_="nhsuk-body-s nhsuk-u-margin-top-1 nhsuk-u-secondary-text-color")

        # Thre's a date associated each to article, adding space to it otherwise it's collated
        count = 1
        ranger = 0
        self.list_of_news = []
        for item in self.lis:
            self.list_of_news.append(item)
            item = item.text
            item = item.replace(self.removing_dates[ranger].text, ":  " + self.removing_dates[ranger].text)
            self.mylist.insert(count, item)
            count += 1
            ranger += 1
        # Designing buttons: View, Back, Forward
        self.view = Button(self.articles, command=lambda: self.view_articles(self.page_number), padx=4, pady=9,
                           text="View article", cursor="tcross", relief="raised")
        self.view.place(x=487, y=465, width=80, height=30)
        # button state can be modified later when user is not on page one
        self.back = Button(self.articles, command=lambda: self.go_back(self.url_number, self.page_number), padx=4,
                           pady=9, text="Previous", cursor="tcross", relief="raised", state="disabled")
        self.back.place(x=87, y=465, width=80, height=30)

        self.next = Button(self.articles, command=lambda: self.next_(self.url_number, self.page_number, self.back),
                           padx=4, pady=9, text="Next", cursor="tcross", relief="raised", state="normal")
        self.next.place(x=627, y=465, width=80, height=30)
        # status bar
        self.status_bar = Label(self.articles,
                                text="Page number: " + str(self.page_number) + " out of " + str(self.max), bg="gray")
        self.status_bar.place(x=15, y=500)

    def view_articles(self, a):
        self.page_number = a
        try:
            self.index = self.mylist.curselection()[0]
        except:
            messagebox.showinfo("Requirement", "Please select an article")
        self.object = self.list_of_news[self.index]
        self.object = self.object.find("a")
        self.object = str(self.object['href'])
        self.object = "https://www.nhs.uk/" + self.object
        self.art = Frame(self.canvas, bg="gray")
        self.art.place(relwidth=800, relheight=485, relx=0.0, rely=0.05)

        self.toolbar = Frame(self.art)

        def home():
            self.fetch()

        self.Back = Button(self.toolbar, text="⇦", command=home)
        self.Back.pack(side=LEFT)
        self.toolbar.pack(side=TOP, fill=X)

        # Find all is used because both the header and lower text have the same class name
        self.output = sc.ScrolledText(self.art, bd=4, wrap=WORD)
        self.output.place(height=480, width=800, x=0, y=27)
        ######################################### Fetching url needs to be done using selenium since it is dynamically generated using javascript so xpath is required
        self.actual_article(self.object)

    def actual_article(self, object):
        self.object = object
        driver.get(self.object)
        self.real = WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.CLASS_NAME, "nhsuk-main-wrapper"))).text
        self.wait = WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.CLASS_NAME, "nhsuk-panel")))
        self.bin = driver.find_element(by=By.XPATH, value='//*[@class="nhsuk-panel"]').text

        # self.bin represents the links at the bottom that are not required
        self.output.insert(INSERT, self.real.replace(self.bin, ""))

    def next_(self, number, page_number, back):
        if self.url_number < int(self.max):
            self.url_number += 1
            self.page_number += 1
            self.article_second_frame()
        if self.url_number == int(self.max):
            self.next.config(state="disabled")
        if self.url_number > 1:
            self.back.config(state="normal")

    def go_back(self, number, page_number):
        self.back.config(state="normal")
        self.url_number = number
        if self.url_number > 1:
            self.back.config(state="normal")
            self.url_number -= 1
            self.page_number -= 1
            self.article_second_frame()
        if self.url_number == 1:
            self.back.config(state="disabled")

        if self.url_number > 1:
            self.back.config(state="normal")
class medical_text:
    def __init__(self, canvas, check):
        # create a linked list for medical conditions by assigning them the number of items that match the search then rank them

        self.canvas = canvas
        self.header = check
        #########################################
        self.text = Frame(self.canvas, bg="gray")
        self.text.place(relwidth=800, relheight=500, rely=0.05)
        self.toolbar = Frame(self.text)

        def home():
            searching_frame.tkraise()

        self.Back = Button(self.toolbar, text="⇦", command=home)
        self.Back.pack(side=LEFT)
        self.toolbar.pack(side=TOP, fill=X)
        ################################################################
        # will find position of the name within useroptions then match its index to urls
        self.position = UserOptions.index(self.header)
        self.getting_text_ = list_of_issues[self.position]
        self.getting_text(self.getting_text_)

    def getting_text(self, link):
        self.link = requests.get(link)
        self.health_link = self.link.content
        self.health_link_two = BeautifulSoup(self.health_link, 'html.parser')
        # fetches other items within a page e.g. treatments or symptoms
        self.official_options = []
        self.official_urls = []
        # scrape options to condition if there are any
        try:
            self.cats = self.health_link_two.find(class_="nhsuk-contents-list__list")
            self.cati = self.cats.find_all(class_="nhsuk-contents-list__link")
            for item in self.cati:
                self.official_options.append(item.text)
                self.official_urls.append("https://www.nhs.uk/" + item["href"])
        except:
            pass

        self.health_link_two = self.health_link_two.findAll(class_="nhsuk-grid-column-two-thirds")
        self.texting = ""

        for i in self.health_link_two:
            i = i.get_text()
            # i is now equal to the text of the class
            self.texting += i

        def bookmark():
            if authenticated == True:  # Prevents NameError - Document change
                self.thread_one = threading.Thread(target=self.add_bookmark)
                self.thread_one.start()
            else:
                messagebox.showinfo("Bookmarks", "In order to create a bookmark you must be logged in")

        self.add = Button(self.text, text="+", relief=RAISED, padx=7, command=bookmark)
        self.add.place(x=765, y=46)
        self.output = sc.ScrolledText(self.text, bd=4, wrap=WORD)
        self.output.place(height=470, width=760, x=0, y=46)
        self.output.insert(INSERT, self.texting)

        # menu to scrape options of condition - if it exists
        self.menu_button = Menubutton(self.text, text="☰", relief=RAISED, padx=5, pady=5)
        self.menu_button.pack()
        self.menu_button.place(x=765, y=80, width=32)
        self.menu = Menu(self.menu_button)
        self.menu_button["menu"] = self.menu

        self.count = 0
        for item in self.official_options:
            self.value = self.official_urls[self.count]
            self.menu.add_command(label=item, command=lambda: self.getting_text(self.value))
            self.count += 1

    def add_bookmark(self):
        global bookmarks
        global authenticated
        self.bookmarks = bookmarks
        self.bool = False

        if authenticated == True and self.header not in bookmarks:
            self.conn = sqlite3.connect('linked tables_two', timeout=10)
            self.c = self.conn.cursor()
            self.c.execute("SELECT ID FROM Details WHERE email_address = '%s' " % email_of_user)
            self.id = []
            for i in self.c:
                self.id.append(i)
            self.id = self.id[0][0]

            self.bookmarks = list(bookmarks)
            self.bookmarks.append(self.header)

            self.string = json.dumps(self.bookmarks)
            self.c.execute("UPDATE Activities SET Bookmarks = (?) WHERE id = (?) ", (self.string, int(self.id)))

            menu.add_command(label=self.header, command=lambda: medical_text(self.canvas, self.header))
            messagebox.showinfo("Bookmarks", "Bookmark has been successfully created")
            self.bookmarks = self.c.execute("SELECT bookmarks FROM Activities where ID = (?)", (ID,))
            self.bookmarks = self.bookmarks.fetchall()

            if type(self.bookmarks[0][
                        0]) == str:  # assuming the list has already had a condition added to it and has therefore been converted into json, we need to fetch that specifc value and decode it
                bookmarks = json.loads(self.bookmarks[0][0])
            else:
                bookmarks = []

            self.conn.commit()
            self.conn.close()
            self.bool = True

        if self.header in bookmarks and self.bool == False:
            messagebox.showinfo("Warning", "This medical condition has been previously bookmarked")
class calendar():
    def __init__(self, canvas):
        if authenticated == True:
            self.dates = Dates
            self.conn = sqlite3.connect('linked tables_two', timeout=10)
            self.c = self.conn.cursor()
            if self.dates[0][0] == None:
                self.dates = {}
            else:
                # import ast
                self.dates = json.loads(Dates[0][0])
                self.dates = ast.literal_eval(self.dates)  # converts it back into dictionary from string
        else:
            messagebox.showinfo("Request", "Log in/Sign up to continue")
            return (None)
        self.canvas = canvas
        # creating sign up frame
        self.calendar = Frame(self.canvas, bg="gray")
        self.calendar.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)

        # Bookmarks:
        self.book = Button(self.calendar, padx=2, width=30, text="Book", relief="raised", cursor="tcross", bg="#add8e6",
                           command=self.book)
        self.book.pack()
        self.book.place(x=20, y=150)

        self.delete = Button(self.calendar, padx=2, width=30, text="Delete event", relief="raised", cursor="tcross",
                             bg="#add8e6", command=self.delete_bookmark)
        self.delete.pack()
        self.delete.place(x=20, y=200)

        self.event = Button(self.calendar, padx=2, width=30, text="Event check", relief="raised", cursor="tcross",
                            bg="#add8e6", command=self.event_check)
        self.event.pack()
        self.event.place(x=20, y=250)

        self.date = Calendar(self.calendar, borderwidth=4)
        self.date.pack(padx=10, pady=10)
        self.date.place(x=350, y=95, height=220)

        self.delete_mail = Button(self.calendar, padx=2, text="Change my email ", relief="raised", cursor="tcross",
                                  command=self.remove_token)
        self.delete_mail.pack()
        self.delete_mail.place(x=630, y=47)
        # Calendar widget will be coloured in by recreating the events - as calendar widget is not stored into table.
        for i in self.dates:
            if type(i) != list and len(self.dates[i]) != 0:
                #from datetime import datetime
                self.datetime_date = datetime(int(i[0:4]),int(i[5:7]),int(i[8:10]))
                self.date.calevent_create(self.datetime_date , "Day",
                                          "")
    def book(self):
        # Creating frame which will request name of event
        self.enter_name = Frame(self.canvas, bg="gray")
        self.enter_name.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)

        self.event_name = Entry(self.enter_name, width=70, borderwidth="7")
        self.event_name.pack()
        self.event_name.place(x=197, y=240)
        # label
        self.event_name_label = Label(self.enter_name, width=61, text="Name of event:")
        self.event_name_label.pack()
        self.event_name_label.place(x=200, y=200)

        def home():
            self.calendar.tkraise()
            return (None)

        self.toolbar = Frame(self.enter_name)
        self.Back = Button(self.toolbar, text="⇦", command=home)
        self.Back.pack(side=LEFT)
        self.toolbar.pack(side=TOP, fill=X)

        self.condition_button = Button(self.enter_name, text="Confirm", command=self.confirming, cursor="tcross")
        self.condition_button.pack()
        self.condition_button.place(x=592, y=280)
    def confirming(self):
        self.fetch = str(self.date.selection_get())
        # Calendar widget will automatically colour event
        self.book = self.date.calevent_create(self.date.selection_get(), "Day",
                                              self.event_name.get())  # Fetches selected day and events can be multiple as stored in list
        if str(
                self.date.selection_get()) in self.dates:  # If date already exists
            self.dates[self.fetch].append(self.event_name.get())
        if str(self.date.selection_get()) not in self.dates:  # If date has not had an event booked for it yet
            self.dates[self.fetch] = [self.event_name.get()]

        self.converted = json.dumps(str(self.dates))

        self.id = ID
        self.c.execute("UPDATE Activities SET Dates = (?) WHERE id = (?) ", (self.converted, int(self.id)))
        self.conn.commit()
        self.returned = messagebox.askyesno("Return",
                                            "Message booked, Would you like the bookmark to also be synced with your GMAIL account?")
        if self.returned == True:
            for i in self.dates:
                if type(i) != list and len(self.dates[i]) != 0:
                    # from datetime import datetime
                    self.datetime_date = datetime(int(i[0:4]), int(i[5:7]), int(i[8:10]))
                    self.date.calevent_create(self.datetime_date, "Day",
                                              "")
            self.google_bookmark()
        else:
            for i in self.dates:
                if type(i) != list and len(self.dates[i]) != 0:
                    # from datetime import datetime
                    self.datetime_date = datetime(int(i[0:4]), int(i[5:7]), int(i[8:10]))
                    self.date.calevent_create(self.datetime_date, "Day",
                                              "")
            self.calendar.tkraise()  # Raises frame backup without deleting new data
    def google_bookmark(self):
        # Has the user linked their gmail account to the application - if not they are automatically prompted to do so.
        self.serivce = calendar_quickstart.main()
        self.confirm(self.serivce)
    def confirm(self, service):
        self.new_date = str(self.date.selection_get()).replace("/", ("-"))
        event = {
            'summary': self.event_name.get(),
            'start': {
                'dateTime': self.new_date + 'T00:00:00-00:00',
                'timeZone': 'Europe/London',
            },
            'end': {
                'dateTime': self.new_date + 'T00:00:00-00:00',
                'timeZone': 'Europe/London',
            },

        }
        self.service = service
        event = self.service.events().insert(calendarId='primary', body=event).execute()

        messagebox.showinfo("Event", "Event successfully booked")
        self.calendar.tkraise()
        return (None)
    def remove_token(self):
        os.system("del /f token_one.pickle")  # deletes if one exists already
        self.serivce = calendar_quickstart.main()
        messagebox.showinfo("Gmail", "Gmail account successfully changed")
    def event_check(self):
        self.send = ""
        if str(self.date.selection_get()) not in self.dates :
            messagebox.showinfo("Gmail", "No events scheduled for this date")
            return (None)
        if len(self.dates[str(self.date.selection_get())]) == 0:
            messagebox.showinfo("Gmail", "No events scheduled for this date")
            return (None)
        else:
            for i in self.dates[str(self.date.selection_get())]:
                self.send += i + "," + "\n"

            messagebox.showinfo("Gmail", "Events scheduled on this date: " + self.send)
    def delete_bookmark(self):
        # Top level will not be created if there are no events scheduled for the day
        if str(self.date.selection_get()) not in self.dates or len(self.dates[str(self.date.selection_get())]) == 0: # Also run even if date exists as it may not have events scheduled
            messagebox.showinfo("Gmail", "No events scheduled for this date")
            self.calendar.tkraise()
            return (None)
        # Creating a top level and setting it's maximum and minimum size
        self.message = Toplevel(width=350, height=200)
        self.message.minsize(width=350, height=200)
        self.message.maxsize(width=350, height=200)
        # label for combobox
        self.label = Label(self.message, width=30, text="Event name: ")
        self.label.pack()
        self.label.place(x= 70, y= 30)
        # List of options
        self.combo = ttk.Combobox(self.message, values=self.dates[str(self.date.selection_get())], width=20)
        self.combo.pack()
        self.combo.place(x= 105, y= 50)
        # Delete button
        self.delete_button = Button(self.message, text="delete", relief=RAISED, padx=5, pady=5,cursor="tcross",command = self.final_removal)
        self.delete_button.pack()
        self.delete_button.place(x= 278, y= 120, width= 45)
        self.message.tkraise()
    def final_removal(self):
        self.id = ID
        try:
            self.dates[str(self.date.selection_get())].remove(self.combo.get())
        except ValueError:
            messagebox.showwarning("Fail", "Select an option to continue")
            return (None)
        self.converted = json.dumps(str(self.dates))
        try:
            self.c.execute("UPDATE Activities SET Dates = (?) WHERE id = (?) ", (self.converted, int(self.id)))
            self.conn.commit()
        except:
            messagebox.showwarning("Fail", "Unsuccessful, please try again later")
            return (None)

        self.date = Calendar(self.calendar, borderwidth=4)
        self.date.pack(padx=10, pady=10)
        self.date.place(x=350, y=95, height=220)

        for i in self.dates:
            if type(i) != list and len(self.dates[i]) != 0:
                # from datetime import datetime
                self.datetime_date = datetime(int(i[0:4]), int(i[5:7]), int(i[8:10]))
                self.date.calevent_create(self.datetime_date, "Day",
                                          "")

        self.message.destroy()
        self.calendar.tkraise()
        messagebox.showinfo("Gmail", "Bookmark successfully deleted")
        return (None)
class email():
    def __init__(self, canvas):
        if authenticated == False:
            messagebox.showinfo("Return", "Log in or Sign up")
            return (None)  # Error at the end -- systematic checks -- record screen
        global GMAIL
        self.table_email = GMAIL[0][0]  # = None if nothing saved into it

        if self.table_email == None:
            self.value = messagebox.askyesno("Return", "Gmail account needs to be linked, would you like to proceed?")
            if self.value:
                os.system("del /f token.pickle")  # deletes if one exists already
                # Error testing

                self.service = quickstart.main()
                self.user = self.service.users().getProfile(userId='me').execute()
                self.user = self.user['emailAddress']
                ######################################################################

                conn = sqlite3.connect('linked tables_two', timeout=10)
                c = conn.cursor()
                # selecting email address - to check if account already exists
                global ID
                self.id = ID
                c.execute("UPDATE Activities SET Gmail = (?) WHERE id = (?)", (self.user, int(self.id)))
                conn.commit()
                conn.close()

            else:
                searching_frame.tkraise()
                return (None)

        self.service = quickstart.main()
        self.user = self.service.users().getProfile(userId='me').execute()
        self.user = self.user['emailAddress']

        self.canvas = canvas
        # creating sign up frame
        self.email = Frame(self.canvas, bg="gray")
        self.email.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)
        # Create email address entry - this will be used to fetch the user's gmail if they have not saved theirs into the database

        # Create email address entry
        self.email_adress = Entry(self.email, width=70, bg="white", borderwidth="9")
        self.email_adress.pack()
        self.email_adress.place(x=300, y=77)
        self.email_adress.insert(0, "helpdesk@nhs.net")
        self.email_adress.config(state="disabled")
        # Create email address label
        self.email_label = Label(self.email, width=30, text="Recipent email:")
        self.email_label.pack()
        self.email_label.place(x=70, y=82)
        # Create password entry
        self.subject = Entry(self.email, width=70, bg="white", borderwidth="9")
        self.subject.pack()
        self.subject.place(x=300, y=120)
        # Create password label
        self.subject_label = Label(self.email, width=30, text="Subject name:")
        self.subject_label.pack()
        self.subject_label.place(x=70, y=124)
        # Button to lead to next page

        self.authenticate = Button(self.email, padx=2, text="Send", relief="raised", cursor="tcross",
                                   command=self.authentication)
        self.authenticate.pack()
        self.authenticate.place(x=660, y=450)

        self.delete_mail = Button(self.email, padx=2, text="Change my email ", relief="raised", cursor="tcross",
                                  command=self.delete)
        self.delete_mail.pack()
        self.delete_mail.place(x=630, y=47)

        self.text = Text(self.email, width=65, height=19, bg="white", borderwidth="3")
        self.text.pack()
        self.text.place(x=70, y=160)

    def authentication(self):

        self.fetch = self.text.get("1.0", END)
        self.message = MIMEText(self.fetch)
        self.message['to'] = "helpdesk@nhs.net"
        self.title = self.subject.get()
        self.message['subject'] = self.title

        self.raw = base64.urlsafe_b64encode(self.message.as_bytes())
        self.raw = self.raw.decode()
        self.body = {'raw': self.raw}
        try:
            message = (self.service.users().messages().send(userId="me", body=self.body)
                       .execute())
            messagebox.showinfo("Pass", "Message successfully sent")
        except:
            messagebox.showwarning("Incorrect", "Please check your details and try again")
            email(self.canvas)
            return (None)
        # This is used to fetch email address used in quickstart

    def delete(self):
        os.system("del /f token.pickle")  # deletes if one exists already
        conn = sqlite3.connect('linked tables_two', timeout=10)
        c = conn.cursor()
        # selecting email address - to check if account already exists
        global ID
        self.id = ID
        self.service = quickstart.main()
        self.user = self.service.users().getProfile(userId='me').execute()
        self.user = self.user['emailAddress']
        if self.user != self.table_email:  # only runs if gmail hasnt been saved into the database or email provided is different
            conn = sqlite3.connect('linked tables_two', timeout=10)
            c = conn.cursor()
            # selecting email address - to check if account already exists
            c.execute("UPDATE Activities SET Gmail = (?) WHERE id = (?)", (self.user, int(self.id)))
            conn.commit()
            conn.close()
class Homepage(Tk):
    def __init__(self, win):
        self.win = win
        self.win.maxsize(width=800, height=550)
        self.win.title("Healthcare")
        self.canvas = Canvas(self.win, width=800, height=550, bg="#808080")
        self.canvas.pack()
        self.authorise = Frame(self.canvas, bg="white")
        self.authorise.place(relwidth=800, relheight=50)
        #######################################################################
        self.frame = Frame(self.canvas, bg="gray")
        self.frame.place(relwidth=800, relheight=500, rely=0.05)
        # creating menu
        self.menu = Menu(self.win)
        self.win.config(menu=self.menu)
        self.sub = Menu(self.menu)
        self.menu.add_cascade(label="Menu", menu=self.sub)
        self.sub.add_command(label="Homepage", command=lambda: self.frame.tkraise())
        self.sub.add_command(label="Latest News", command=lambda: medical_articles(self.canvas))
        self.sub.add_command(label="Symptom Searcher", command=lambda: symptom(self.canvas))
        self.sub.add_command(label="Email", command=lambda: email(self.canvas))
        self.sub.add_command(label="Calendar", command=lambda: calendar(self.canvas))
        # widgets in homepage frame ---- ------------------------------
        # search bar
        self.search_conditions = Entry(self.frame, width=70, bg="cyan", fg="blue", borderwidth="7")
        self.search_conditions.pack()
        self.search_conditions.place(x=197, y=240)
        # label

        self.search_label = Label(self.frame, width=61, text="Search for a condition")
        self.search_label.pack()
        self.search_label.place(x=200, y=200)
        # button for logging in and signing up
        self.login = Button(self.authorise, text="Login", width=8, height=1, command=lambda: login(self.canvas))
        self.login.grid(row=0, column=0, ipadx=2, ipady=1)
        self.signup = Button(self.authorise, text="Sign up", width=8, height=1, command=lambda: sign_up(self.canvas))
        self.signup.grid(row=0, column=1, ipadx=2, ipady=1)
        global menu
        self.menu_button = Menubutton(self.frame, text="☰", relief=RAISED, padx=5, pady=5)
        self.menu_button.pack()
        self.menu_button.place(x=765, y=60, width=32)
        self.menu = Menu(self.menu_button)
        self.menu_button["menu"] = self.menu
        menu = self.menu
        global searching_frame
        searching_frame = self.frame

        def f():
            def raise_frame(value_given):
                taken = value_given
                ###################################
                values_for_combobox = []
                self.algorithm_fetch = order.ordering(taken, UserOptions, list_of_issues)
                self.algorithm_fetch = self.algorithm_fetch.options
                combo = ttk.Combobox(self.frame, values=self.algorithm_fetch, width=40)
                combo.pack()
                combo.place(x=200, y=280)
                global information

                def fetch():
                    try:
                        next_step = medical_text(self.canvas, combo.get())
                    except:
                        self.frame.tkraise()
                        messagebox.showinfo("Selection", "Please choose a medical condition")

                found = Button(self.frame, text="Output", cursor="tcross", command=fetch)
                found.pack()
                found.place(x=500, y=280)

            value_given = self.search_conditions.get()
            raise_frame(value_given)

        self.condition_button = Button(self.frame, text="search", command=f, cursor="tcross")
        self.condition_button.pack()
        self.condition_button.place(x=592, y=280)
        win.mainloop()
class background():
    def __init__(self):
        global UserOptions
        global list_of_issues
        # global variables are messing up my code
        UserOptions = []
        list_of_issues = []
        self.nhs = requests.get("https://www.nhs.uk/conditions/")
        self.health = self.nhs.content
        self.health_two = BeautifulSoup(self.health, 'html.parser')
        self.links = self.health_two.find("ol", class_="nhsuk-list")
        self.links = self.links.findAll("a", class_="nhsuk-list-panel__link")
        for item in self.links:
            list_of_issues.append("https://www.nhs.uk" + item.get("href"))
            UserOptions.append(item.text)
        ################ Ended recursrion error, doesn't keep going on forever - remove and add into documentation
        ##########################################################################
        ##########################################################################
class symptom():
    def __init__(self, canvas):
        self.canvas = canvas
        # creating symptom frame
        self.log = Frame(self.canvas, bg="gray")
        self.log.place(relwidth=800, relheight=500, relx=0.0, rely=0.05)
        self.title = Label(self.log, text="Symptom Searcher", relief="sunken", bg="cyan", padx=6, pady=6)
        self.title.place(y=20, height=34, width=500, x=160)
        self.label = Label(self.log, text="Symptom Name:", padx=12)
        self.label.place(y=120, x=90)
        self.symptom_name = Entry(self.log, width=42)
        self.symptom_name.place(y=120, x=220)

        self.options_label = Label(self.log, text="Matching values: ", padx=12)
        self.options_label.place(y=155, x=90)
        self.options = Listbox(self.log, width=50)
        self.options.place(y=200, x=90, height=260)

        self.added_pointer = 0 # used to navigate listbox
        self.added_values_label = Label(self.log, text="Added: ", padx=12)
        self.added_values_label.place(y=155, x=400)
        self.added_values = Listbox(self.log, width=50)
        self.added_values.place(y=200, x=400, height=260)
        # Top level will ask for the user's sex and age
        self.message = Toplevel(width=350, height=200)
        self.gender = Label(self.message, text="Are you male or female:")
        self.gender.place(y=2, x=20)
        self.gender_options = Listbox(self.message, width=50, height=2)
        self.gender_options.place(y=30, x=20)
        self.gender_options.insert(0, "Male")
        self.gender_options.insert(1, "Female")
        self.age = Label(self.message, text="Enter your age:")
        self.age.place(y=80, x=20)

        self.entry = Entry(self.message)
        self.entry.place(y=80, x=120)
        self.message.grab_set()  # when you show the popup

        # Button to move onto the text page
        self.button = Button(self.message, text="Continue", relief="raised", command=self.fetch, cursor="tcross")
        self.button.place(y=150, x=261)

        # Button to remove added symptom
        self.button = Button(self.log, text="Remove added symptom", relief="raised", command=self.remove, cursor="tcross")
        self.button.place(y= 470, x= 450)

        # Button to output corresponding symptoms
        self.search = Button(self.log, text="Search medical symptom", padx=12, cursor="tcross", command= self.scrape)
        self.search.place(y=470, x=91)
        self.finish = Button(self.log, text="Continue", padx=13, cursor="tcross", bg = "#add8e6", command= self.testing,state = "disabled")
        self.finish.place(y=470, x=620)

        self.add_condition = Button(self.log, text="Add symptom", padx=12, cursor="tcross", command=self.add)
        self.add_condition.place(y=470, x=300)
    def fetch(self):
        try:
            self.actual_gender = self.gender_options.curselection()[0]
            self.age_gotten = int(self.entry.get())
        except:
            messagebox.showinfo("Warning", ("Please select a gender and an appropriate age"))
            self.message.destroy()
            self.a = symptom(self.canvas)
            return (0)

        if self.age_gotten > 0 and self.age_gotten < 126:
            self.message.destroy()
            self.communcicate = threading.Thread(target=self.close)
            self.communcicate.start()
        else:
            messagebox.showinfo("Warning", ("Please select a gender and an appropriate age"))
            self.message.destroy()
            symptom(self.canvas)
            return (0)
    def close(self):

        driver.get("https://symptoms.webmd.com/")
        WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.ID, "age")))
        driver.find_element(By.ID, "age").send_keys(self.age_gotten)
        if self.actual_gender == 0:
            driver.find_element(By.ID, "male").click()
        else:
            driver.find_element(By.ID, "female").click()
        WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.XPATH, '//*[@class="webmd-button solid-button continue-button info-button webmd-button--primary webmd-button--medium"]')))
        driver.find_element(by=By.XPATH,
                            value='//*[@class="webmd-button solid-button continue-button info-button webmd-button--primary webmd-button--medium"]').click()

        return (None)
    def scrape(self):
        WebDriverWait(driver, 10).until(
            EC.presence_of_element_located((By.XPATH,
                                            '//*[@class="form-control type-ahead-select taller"]')))
        self.count = 0  # index of listbox
        driver.find_element(by=By.XPATH, value='//*[@class="form-control type-ahead-select taller"]').send_keys(
            Keys.CONTROL + "a")  # Selects all text within text field
        driver.find_element(by=By.XPATH, value='//*[@class="form-control type-ahead-select taller"]').send_keys(
            Keys.DELETE)
        driver.find_element(by=By.XPATH, value='//*[@class="form-control type-ahead-select taller"]').send_keys(
            self.symptom_name.get())
        # Wait until drop down menu is created
        self.menu = WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.ID, "resultContainer")))
        self.menu = driver.find_element(by=By.ID, value="resultContainer")
        time.sleep(2)
        try:
            self.lis = self.menu.find_elements(by=By.TAG_NAME, value="li")
        except:
            time.sleep(2)
            self.lis = self.menu.find_elements(by=By.TAG_NAME, value="li")

        for item in self.lis:
            if item.text != "Can’t find your symptom? Only some symptoms are factored into results.":
                self.options.insert(self.count, item.text)
                self.count += 1
            else:
                pass
    def add(self):
        try:
            self.index = self.options.curselection()[0]
        except:
            messagebox.showinfo("Symptom","Symptom needs to be selected before proceeding.")
            return (None)

        # Item is added to the listbox on the right
        self.added_values.insert(self.added_pointer, self.lis[self.index].text)
        self.added_pointer += 1
        # selenium is used to click on element
        self.menu.find_elements(by=By.TAG_NAME, value="li")[self.index].click()

        self.finish.config(state = "normal")
        try:
            self.options.delete(0, "end") # deleting content inside listbox
        except:
            pass
    def remove(self):
        try:
            # # Item selected in added listbox
            self.index = self.added_values.curselection()[0]
        except:
            messagebox.showinfo("Symptom", "Symptom needs to be selected before proceeding.")
            return (None)

        self.execute = "document.getElementsByClassName('delete-icon')[%s].click()"%((self.index),)
        driver.execute_script(self.execute)
        self.added_values.delete(self.index)
        if self.added_values.size() == 0:
            self.finish.config(state="disabled")
    def testing(self):
        # Checking if symptoms are present
        try:
            time.sleep(1)
            driver.execute_script("document.getElementsByClassName('solid-button continue-button')[0].click()")
        except:
            time.sleep(2)
            driver.execute_script("document.getElementsByClassName('solid-button continue-button')[0].click()")
        # There's another continue button
        try:
            time.sleep(1)
            driver.execute_script("document.getElementsByClassName('solid-button continue-button')[0].click()")
        except:
            time.sleep(2)
            driver.execute_script("document.getElementsByClassName('solid-button continue-button')[0].click()")


        try:
            self.result = driver.execute_script("return document.getElementsByClassName('noSymptomtext')[0].innerText")
            # code above throws error if element does not exist - meaning enough symptoms have been added
            if self.result == "We are unable to find any conditions that match the symptoms you entered.":
                driver.execute_script("document.getElementsByClassName('noSymptomLink')[0].click()")
                messagebox.showinfo("Return", "Not enough symptoms added")
        except:
            self.new_frame()
    def new_frame(self):

        self.top = Frame(self.canvas, bg="gray")
        self.top.place(relwidth=800, relheight=500, rely=0.05)

        # Label for conditions:
        self.title = Label(self.top, text="Conditions that match your symptoms:", relief="sunken", bg="cyan", padx=6, pady=6)
        self.title.place(y=120, height=34, width= 270, x= 40)

        self.output = sc.ScrolledText(self.top, bd=4, wrap=WORD)
        self.output.place(height=440, width= 460, x= 320, y= 66)


        self.elements = driver.execute_script("return document.getElementsByClassName('single-condition-row')")
        self.items = []
        for i in self.elements:
            i = i.text.replace("Fair match","")
            self.items.append(i)
        # new import for combobox
        self.medical = Combobox(self.top, width=27)

        # Adding combobox drop down list
        self.medical['values'] = self.items

        self.medical.place(y = 175, x = 41)


        self.condition_button = Button(self.top, text="search",command = self.select,cursor="tcross")
        self.condition_button.pack()
        self.condition_button.place(x= 230, y= 220)
        # Details or Treatment
        self.R2 = Radiobutton(self.top,text="Treatment", value=2,command = lambda: self.not_truth())
        self.R2.place(x=385, y=35)

        self.R1 = Radiobutton(self.top,text="Details", value=1,command = lambda: self.select()
                         )
        self.R1.place(x = 320, y = 35)
    def not_truth(self):
        if self.medical.current() == -1:
            messagebox.showinfo("Symptoms", "Condition required")
            return (None)
        driver.execute_script("document.getElementsByClassName('solid-button continue-button treatment-option-button')[0].click()" )
        time.sleep(2)
        self.current = driver.find_element(By.CLASS_NAME, "condition-article").text
        self.output = sc.ScrolledText(self.top, bd=4, wrap=WORD)
        self.output.place(height=440, width=460, x=320, y=66)
        self.output.insert(INSERT, self.current)
    def select(self):
        if self.medical.current() == -1:
            messagebox.showinfo("Symptoms", "Condition required")
            return(None)

        driver.execute_script("elem = document.getElementsByClassName('single-condition')")
        driver.execute_script("elem[%s].click()"% ((self.medical.current()),))

        time.sleep(2)

        self.current = driver.find_element(By.CLASS_NAME,"condition-article").text
        self.output = sc.ScrolledText(self.top, bd=4, wrap=WORD)
        self.output.place(height=440, width=460, x=320, y=66)
        self.output.insert(INSERT, self.current)
        self.R1.select()

if __name__ == "__main__":

    chrome_options = Options()
    chrome_options.add_argument('--headless')
    chrome_options.add_experimental_option("prefs", {"profile.default_content_setting_values.cookies": 2})

    driver = webdriver.Chrome(options=chrome_options)

    authenticated = False
    win = Tk()
    list_of_issues_process = threading.Thread(target=background)
    list_of_issues_process.start()
    Homepage(win)
