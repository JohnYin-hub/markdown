# **🗓️ Day 1**

## Setting up a local development environment

Before we can actually start building Streamlit apps, we will first have to setup a development environment.

Let's start by installing and setting up a conda environment.

## **Install conda**

- Install `conda` by going to https://docs.conda.io/en/latest/miniconda.html and choose your operating system (Windows, Mac or Linux).
- Download and run the installer to install `conda`.

## **Create a new conda environment**

Now that you have conda installed, let's create a conda environment for managing all the Python library dependencies.

To create a new environment with Python 3.9, enter the following:

```bash
conda create -n stenv python=3.9
```

where `create -n stenv` will create a conda environment named `stenv` and `python=3.9` will setup the conda environment with Python version 3.9.

## **Activate the conda environment**

To use a conda environment that we had just created that is named `stenv`, enter the following into the command line:

```bash
conda activate stenv
```

## **Install the Streamlit library**

It's now time to install the `streamlit` library:

```bash
pip install streamlit
```

## **Launching the Streamlit demo app**

To launch the Streamlit demo app (Figure 1) type:

```bash
streamlit hello
```

### Figures

![0](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/3876bb40e352fe047681d015501a728a9e398892a38089635ebe0799-20221101192540903.png)

Figure 1: Streamlit demo app is launched via "streamlit hello"

# 🗓️ Day 2

## Building your first Streamlit app

## Fire up your IDE

Fire up your IDE whether it be Atom, VS Code or even a cloud IDE such as GitPod or GitHub.dev.

Create a file called `streamlit_app.py`

#### Entering your first lines of code

To the newly created file, enter the following lines of code:

```python
import streamlit as st

st.write('Hello world!')
```

Save the file.

## Fire up the command line terminal

To the terminal, enter the following:

```bash
streamlit run streamlit_app.py
```

A browser window should pop-up showing the newly created Streamlit app.

**Congratulations!** You have just created your first Streamlit app!

Figure2:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221101194551761.png" alt="image-20221101194551761" style="zoom: 33%;" />

# 🗓️ Day 3

## st.button

`st.button` allows the display of a button widget.

## What we're building?

A simple app that performs conditionally prints out alternative messages depending on whether the button was pressed or not.

Flow of the app:

1. By default, the app prints `Goodbye`
2. Upon clicking on the button, the app displays the alternative message `Why hello there`

## Demo app

The deployed Streamlit app should look something like the one shown in the below link:

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white.svg)](https://share.streamlit.io/dataprofessor/st.button/)

## Code

Here's the code to implement the above mentioned app:

```
import streamlit as st

st.header('st.button')

if st.button('Say hello'):
     st.write('Why hello there')
else:
     st.write('Goodbye')
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```
import streamlit as st
```

This is followed by creating a header text for the app:

```
st.header('st.button')
```

Next, we will use conditional statements `if` and `else` for printing alternative messages.

```
if st.button('Say hello'):
     st.write('Why hello there')
else:
     st.write('Goodbye')
```

As we can see from the above code box, the `st.button()` command accepts the `label` input argument of `Say hello`, which is the text that the button displays.

The `st.write` command is used to print text messages of either `Why hello there` or `Goodbye` depending on whether the button was clicked or not, which is implemented via:

```
st.write('Why hello there')
```

```
st.write('Goodbye')
```

It is important to note that the above `st.write` statements are placed under the `if` and `else` conditions in order to perform the above mentioned process of alternative displaying of messages

## Next steps

Now that you have created the Streamlit app locally, it's time to deploy it to [Streamlit Cloud](https://streamlit.io/cloud) as will be explained soon in an upcoming challenge.

Because this is the first week of your challenge, we provide the full code (as shown in the code box above) and solution (the demo app) right inside this webpage.

Moving forward in the next challenges, it is recommended that you first try implementing the Streamlit app yourself.

Don't worry if you get stuck, you can always take a peek at the solution.

Figure3:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221101195345990.png" alt="image-20221101195345990" style="zoom:25%;" /> 

#  🗓️ Day 5

## st.write

`st.write` allows writing text and arguments to the Streamlit app.

In addition to being able to display text, the following can also be displayed via the `st.write()` command:

- Prints strings; works like `st.markdown()`
- Displays a Python `dict`
- Displays `pandas` DataFrame can be displayed as a table
- Plots/graphs/figures from `matplotlib`, `plotly`, `altair`, `graphviz`, `bokeh`
- And more (see [st.write on API docs](https://docs.streamlit.io/library/api-reference/write-magic/st.write))

## What we're building?

A simple app showing the various ways on how to use the `st.write()` command for displaying text, numbers, DataFrames and plots.

## Demo app

The deployed Streamlit app should look something like the one shown in the below link:

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221101201326427.svg)](https://share.streamlit.io/dataprofessor/st.write/)

## Code

Here's how to use st.write:

```python
import numpy as np
import altair as alt
import pandas as pd
import streamlit as st

st.header('st.write')

# Example 1

st.write('Hello, *World!* :sunglasses:')

# Example 2

st.write(1234)

# Example 3

df = pd.DataFrame({
     'first column': [1, 2, 3, 4],
     'second column': [10, 20, 30, 40]
     })
st.write(df)

# Example 4

st.write('Below is a DataFrame:', df, 'Above is a dataframe.')

# Example 5

df2 = pd.DataFrame(
     np.random.randn(200, 3),
     columns=['a', 'b', 'c'])
c = alt.Chart(df2).mark_circle().encode(
     x='a', y='b', size='c', color='c', tooltip=['a', 'b', 'c'])
st.write(c)
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```
import streamlit as st
```

This is followed by creating a header text for the app:

```
st.header('st.write')
```

**Example 1** Its basic use case is to display text and Markdown-formatted text:

```
st.write('Hello, *World!* :sunglasses:')
```

**Example 2** As mentioned above, it can also be used to display other data formats such as numbers:

```
st.write(1234)
```

**Example 3** DataFrames can also be displayed as follows:

```
df = pd.DataFrame({
     'first column': [1, 2, 3, 4],
     'second column': [10, 20, 30, 40]
     })
st.write(df)
```

**Example 4** You can pass in multiple arguments:

```
st.write('Below is a DataFrame:', df, 'Above is a dataframe.')
```

**Example 5** Finally, you can also display plots as well by passing it to a variable as follows:

```
df2 = pd.DataFrame(
     np.random.randn(200, 3),
     columns=['a', 'b', 'c'])
c = alt.Chart(df2).mark_circle().encode(
     x='a', y='b', size='c', color='c', tooltip=['a', 'b', 'c'])
st.write(c)
```

## Demo app

The deployed Streamlit app should look something like the one shown in the below link:

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221101201326427.svg)](https://share.streamlit.io/dataprofessor/st.write/)

## Next steps

Now that you have created the Streamlit app locally, it's time to deploy it to [Streamlit Cloud](https://streamlit.io/cloud) as will be explained soon in an upcoming challenge.

Because this is the first week of your challenge, we provide the full code (as shown in the code box above) and solution (the demo app) right inside this webpage.

Moving forward in the next challenges, it is recommended that you first try implementing the Streamlit app yourself.

Don't worry if you get stuck, you can always take a peek at the solution.

Figure4:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221101202724820.png" alt="image-20221101202724820" style="zoom:33%;" />

## Further reading

In addition to [`st.write`](https://docs.streamlit.io/library/api-reference/write-magic/st.write), you can explore the other ways of displaying text:

- [`st.markdown`](https://docs.streamlit.io/library/api-reference/text/st.markdown)
- [`st.header`](https://docs.streamlit.io/library/api-reference/text/st.header)
- [`st.subheader`](https://docs.streamlit.io/library/api-reference/text/st.subheader)
- [`st.caption`](https://docs.streamlit.io/library/api-reference/text/st.caption)
- [`st.text`](https://docs.streamlit.io/library/api-reference/text/st.text)
- [`st.latex`](https://docs.streamlit.io/library/api-reference/text/st.latex)
- [`st.code`](https://docs.streamlit.io/library/api-reference/text/st.code)

# 🗓️ Day 8

## st.slider

`st.slider` allows the display of a slider input widget.

The following data types are supported: int, float, date, time, and datetime.

## What we're building?

A simple app that shows the various ways on how to accept user input by adjusting the slider widget.

Flow of the app:

1. User selects value by adjusting the slider widget
2. App prints out the selected value

## Demo app

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221101202627094.svg)](https://share.streamlit.io/dataprofessor/st.slider/)

## Code

Here's how to use st.slider:

```python
import streamlit as st
from datetime import time, datetime

st.header('st.slider')

# Example 1

st.subheader('Slider')

age = st.slider('How old are you?', 0, 130, 25)
st.write("I'm ", age, 'years old')

# Example 2

st.subheader('Range slider')

values = st.slider(
     'Select a range of values',
     0.0, 100.0, (25.0, 75.0))
st.write('Values:', values)

# Example 3

st.subheader('Range time slider')

appointment = st.slider(
     "Schedule your appointment:",
     value=(time(11, 30), time(12, 45)))
st.write("You're scheduled for:", appointment)

# Example 4

st.subheader('Datetime slider')

start_time = st.slider(
     "When do you start?",
     value=datetime(2020, 1, 1, 9, 30),
     format="MM/DD/YY - hh:mm")
st.write("Start time:", start_time)
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```
import streamlit as st
from datetime import time, datetime
```

This is followed by creating a header text for the app:

```
st.header('st.slider')
```

**Example 1**

Slider:

```python
st.subheader('Slider')

age = st.slider('How old are you?', 0, 130, 25)
st.write("I'm ", age, 'years old')
```

As we can see, the `st.slider()` command is used to collect user input about the age of users.

The first input argument displays the text just above the **slider** widget asking `'How old are you?'`.

The following three integers `0, 130, 25` represents the minimum, maximum and default values, respectively.

**Example 2**

Range slider:

```python
st.subheader('Range slider')

values = st.slider(
     'Select a range of values',
     0.0, 100.0, (25.0, 75.0))
st.write('Values:', values)
```

The range slider allow selection of a lower and upper bound value pair.

The first input argument displays the text just above the **range slider** widget asking `'Select a range of values'`.

The following three arguments `0.0, 100.0, (25.0, 75.0)` represents the minimum and maximum values while the last tuple denotes the default values to use as the selected lower (25.0) and upper (75.0) bound values.

**Example 3**

Range time slider:

```python
st.subheader('Range time slider')

appointment = st.slider(
     "Schedule your appointment:",
     value=(time(11, 30), time(12, 45)))
st.write("You're scheduled for:", appointment)
```

The range time slider allows selection of a lower and upper bound value pair of datetime.

The first input argument displays the text just above the **range time slider** widget asking `'Schedule your appointment:`.

The default values for the lower and upper bound value pairs of datetime are set to 11:30 and 12:45, respectively.

**Example 4**

Datetime slider:

```python
st.subheader('Datetime slider')

start_time = st.slider(
     "When do you start?",
     value=datetime(2020, 1, 1, 9, 30),
     format="MM/DD/YY - hh:mm")
st.write("Start time:", start_time)
```

The datetime slider allows selection of a datetime.

The first input argument displays the text just above the **datetime** slider widget asking `'When do you start?'`.

The default value for the datetime was set using the `value` option to be January 1, 2020 at 9:30

Figure5:

<img src="../../../Library/Application Support/typora-user-images/image-20221101203354404.png" alt="image-20221101203354404" style="zoom: 25%;" />

## Further reading

You can also explore the following related widget:

- [`st.select_slider`](https://docs.streamlit.io/library/api-reference/widgets/st.select_slider)

# 🗓️ Day 9

## st.line_chart

`st.line_chart` displays a line chart.

This is syntax-sugar around `st.altair_chart`. The main difference is this command uses the data's own column and indices to figure out the chart's spec. As a result this is easier to use for many "just plot this" scenarios, while being less customizable.

If `st.line_chart` does not guess the data specification correctly, try specifying your desired chart using st.altair_chart.

## What we're building?

A simple app for displaying a line chart.

Flow of the app:

1. Create a `Pandas` DataFrame from numbers randomly generated via `NumPy`.
2. Create and display the line chart via `st.line_chart()` command.

## Demo app

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/dataprofessor/st.line_chart/)

## Code

Here's how to use [`st.line_chart`](https://docs.streamlit.io/library/api-reference/charts/st.line_chart):



```
import streamlit as st
import pandas as pd
import numpy as np

st.header('Line chart')

chart_data = pd.DataFrame(
     np.random.randn(20, 3),
     columns=['a', 'b', 'c'])

st.line_chart(chart_data)
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` as well as other libraries like so:



```
import streamlit as st
import pandas as pd
import numpy as np
```

Next, we create a header text for the app:



```
st.header('Line chart')
```

Then, we create a DataFrame of randomly generated numbers that contains 3 columns.



```
chart_data = pd.DataFrame(
     np.random.randn(20, 3),
     columns=['a', 'b', 'c'])
```

Finally, a line chart is created by using `st.line_chart()` with the DataFrame stored in the `chart_data` variable as the input data:

```
st.line_chart(chart_data)
```

Figure5:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221101211605212.png" alt="image-20221101211605212" style="zoom:33%;" />

## Further reading

Read more about the following related Streamlit command from which [`st.line_chart`](https://docs.streamlit.io/library/api-reference/charts/st.line_chart) is based on:

- [`st.altair_chart`](https://docs.streamlit.io/library/api-reference/charts/st.altair_chart)

# 🗓️ Day 10

## st.selectbox

`st.selectbox` allows the display of a select widget.

## What we're building?

A simple app that asks the user what their favorite color is.

Flow of the app:

1. User selects a color
2. App prints out the selected color

## Demo app

The deployed Streamlit app should look something like the one shown in the below link:

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221102001518750.svg)](https://share.streamlit.io/dataprofessor/st.selectbox/)

## Code

Here's the code to implement the above mentioned app:



```
import streamlit as st

st.header('st.selectbox')

option = st.selectbox(
     'What is your favorite color?',
     ('Blue', 'Red', 'Green'))

st.write('Your favorite color is ', option)
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:



```
import streamlit as st
```

This is followed by creating a header text for the app:



```
st.header('st.selectbox')
```

Next, we will create a variable called `option` that will accept user input in the form of a **select** input widget via the `st.selectbox()` command.



```
option = st.selectbox(
     'What is your favorite color?',
     ('Blue', 'Red', 'Green'))
```

As we can see from the above code box, the `st.selectbox()` command accepts 2 input arguments:

1. The text that goes above the select widget, i.e. `'What is your favorite color?'`
2. The possible values to select from `('Blue', 'Red', 'Green')`

Finally, we'll print out the selected color as follows:



```
st.write('Your favorite color is ', option)
```

## Next steps

Now that you have created the Streamlit app locally, it's time to deploy it to [Streamlit Cloud](https://streamlit.io/cloud).

Figure6:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221102001635557.png" alt="image-20221102001635557" style="zoom: 33%;" />

## References

More about [`st.selectbox`](https://docs.streamlit.io/library/api-reference/widgets/st.selectbox)

# 🗓️ Day 12

#### st.checkbox

`st.checkbox` displays a checkbox widget.

## Demo app

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221102161103693.svg)](https://share.streamlit.io/dataprofessor/st.checkbox/)

## Code

Here's how to use `st.checkbox`:

```python
import streamlit as st

st.header('st.checkbox')

st.write ('What would you like to order?')

icecream = st.checkbox('Ice cream')
coffee = st.checkbox('Coffee')
cola = st.checkbox('Cola')

if icecream:
     st.write("Great! Here's some more 🍦")

if coffee: 
     st.write("Okay, here's some coffee ☕")

if cola:
     st.write("Here you go 🥤")
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```python
import streamlit as st
```

This is followed by creating a header text for the app:

```python
st.header('st.checkbox')
```

Next, we're going to ask a question via `st.write':

```python
st.write ('What would you like to order?')
```

We're then going to provide some menu items to tick on:

```python
icecream = st.checkbox('Ice cream')
coffee = st.checkbox('Coffee')
cola = st.checkbox('Cola')
```

Finally, we're going to print custom text depending on which checkbox was ticked on:

```python
if icecream:
     st.write("Great! Here's some more 🍦")

if coffee: 
     st.write("Okay, here's some coffee ☕")

if cola:
     st.write("Here you go 🥤")
```

Figure7:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221102163722664.png" alt="image-20221102163722664" style="zoom:33%;" />

## Further reading

- [`st.checkbox`](https://docs.streamlit.io/library/api-reference/widgets/st.checkbox)

# 🗓️ Day 14

#### Streamlit Components

Components are third-party Python modules that extend what's possible with Streamlit [[1](https://docs.streamlit.io/library/components)].

## What Streamlit components are available?

There are several dozens of Streamlit components featured on Streamlit's website [[2](https://streamlit.io/components)].

Fanilo (a Streamlit Creator) curated an amazing list of Streamlit components on a wiki post [[3](https://discuss.streamlit.io/t/streamlit-components-community-tracker/4634)] that lists about 85 Streamlit components as of April 2022.

## How to use?

Streamlit components are just a pip-install away.

In this tutorial, let's get you started in using the `streamlit_pandas_profiling` component [[4](https://share.streamlit.io/okld/streamlit-gallery/main?p=pandas-profiling)].

#### Install the component

```
pip install streamlit_pandas_profiling
```

## Demo app

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221102164047319.svg)](https://share.streamlit.io/dataprofessor/streamlit-components/)

## Code

Here's how to build a Streamlit app using a component:

```python
import streamlit as st
import pandas as pd
import pandas_profiling
from streamlit_pandas_profiling import st_profile_report

st.header('`streamlit_pandas_profiling`')

df = pd.read_csv('https://raw.githubusercontent.com/dataprofessor/data/master/penguins_cleaned.csv')

pr = df.profile_report()
st_profile_report(pr)
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` as well as other libraries used in the app like so:

```python
import streamlit as st
import pandas as pd
import pandas_profiling
from streamlit_pandas_profiling import st_profile_report
```

This is followed by creating a header text for the app:

```python
st.header('`streamlit_pandas_profiling`')
```

Next, we load in the Penguins dataset using the `read_csv` command of `pandas`.

```python
df = pd.read_csv('https://raw.githubusercontent.com/dataprofessor/data/master/penguins_cleaned.csv')
```

Finally, the pandas profiling report is generated via the `profile_report()` command and displayed using `st_profile_report`:

```python
pr = df.profile_report()
st_profile_report(pr)
```

## Making your own Components

If you're interested in making your own component, please check out the following resources:

- [Create a Component](https://docs.streamlit.io/library/components/create)
- [Publish a Component](https://docs.streamlit.io/library/components/publish)
- [Components API](https://docs.streamlit.io/library/components/components-api)
- [Blog post on Components](https://blog.streamlit.io/introducing-streamlit-components/)

Alternatively, if you prefer to learn using videos, our engineer Tim Conkling has put together some amazing tutorials:

- [How to build a Streamlit component | Part 1: Setup and Architecture](https://youtu.be/BuD3gILJW-Q)
- [How to build a Streamlit component | Part 2: Part 2: Make a Slider Widget](https://youtu.be/QjccJl_7Jco)

Figure8:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221102172629289.png" alt="image-20221102172629289" style="zoom:33%;" />

## Further reading about Components

1. [Streamlit Components - API Documentation](https://docs.streamlit.io/library/components)
2. [Featured Streamlit Components](https://streamlit.io/components)
3. [Streamlit Components - Community Tracker](https://discuss.streamlit.io/t/streamlit-components-community-tracker/4634)
4. [`streamlit_pandas_profiling`](https://share.streamlit.io/okld/streamlit-gallery/main?p=pandas-profiling)

# 🗓️ Day 15

#### st.latex

`st.latex` display mathematical expressions formatted as LaTeX.

## What we're building?

A simple app that displays a mathematical equation using LaTeX syntax via the `st.latex` command.

## Demo app

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221103154046731.svg)](https://share.streamlit.io/dataprofessor/st.latex/)

## Code

Here's how to use `st.latex`:

```python
import streamlit as st

st.header('st.latex')

st.latex(r'''
     a + ar + a r^2 + a r^3 + \cdots + a r^{n-1} =
     \sum_{k=0}^{n-1} ar^k =
     a \left(\frac{1-r^{n}}{1-r}\right)
     ''')
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```python
import streamlit as st
```

This is followed by creating a header text for the app:

```python
st.header('st.latex')
```

Next, we're displaying the mathematical equation via `st.latex`:

```python
st.latex(r'''
     a + ar + a r^2 + a r^3 + \cdots + a r^{n-1} =
     \sum_{k=0}^{n-1} ar^k =
     a \left(\frac{1-r^{n}}{1-r}\right)
     ''')
```

Figure9:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221103154319392.png" alt="image-20221103154319392" style="zoom:33%;" />

## References

- Read more about [`st.latex`](https://docs.streamlit.io/library/api-reference/text/st.latex) in the Streamlit API Documentation.

# 🗓️ Day 16

#### Customizing the theme of Streamlit apps

We can customize the theme by adjusting parameters in `config.toml`, which is a configuration file stored in the same folder as the app in the `.streamlit` folder.

## What we're building?

A simple app that shows the result of our theme customization. This is made possible by customizing the HTML HEX code inside the [`.streamlit/config.toml`](https://github.com/dataprofessor/streamlit-custom-theme/blob/master/.streamlit/config.toml) file.

## Demo app

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io/dataprofessor/streamlit-custom-theme/)

## Code

Here's the code to the [`streamlit_app.py`](https://github.com/dataprofessor/streamlit-custom-theme/blob/master/streamlit_app.py) file:

```
import streamlit as st

st.title('Customizing the theme of Streamlit apps')

st.write('Contents of the `.streamlit/config.toml` file of this app')

st.code("""
[theme]
primaryColor="#F39C12"
backgroundColor="#2E86C1"
secondaryBackgroundColor="#AED6F1"
textColor="#FFFFFF"
font="monospace"
""")

number = st.sidebar.slider('Select a number:', 0, 10, 5)
st.write('Selected number from slider widget is:', number)
```

Here's the code to the [`.streamlit/config.toml`](https://github.com/dataprofessor/streamlit-custom-theme/blob/master/.streamlit/config.toml) file:

```
[theme]
primaryColor="#F39C12"
backgroundColor="#2E86C1"
secondaryBackgroundColor="#AED6F1"
textColor="#FFFFFF"
font="monospace"
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```
import streamlit as st
```

This is followed by creating a title text for the app:

```
st.title('Theming with config.toml')
```

Next, we're going to show the contents of the `.streamlit/config.toml` file which we'll first display a note of this via `st.write` followed by the actual code via `st.code`:

```
st.write('Contents of the ./streamlit/config.toml file of this app')

st.code("""
[theme]
primaryColor="#F39C12"
backgroundColor="#2E86C1"
secondaryBackgroundColor="#AED6F1"
textColor="#FFFFFF"
font="monospace"
""")
```

Finally, we're creating a slider widget in the sidebar followed by displaying the selected number:

```
number = st.sidebar.slider('Select a number:', 0, 10, 5)
st.write('Selected number from slider widget is:', number)
```

Let's now take a look at the custom colors that we've used in this app, which is specified in the `.streamlit/config.toml` file:

- `primaryColor="#F39C12"` - This sets the primary color to orange. Notice the orange colors in the slider widget.
- `backgroundColor="#2E86C1"` - This sets the background color to blue. Notice the main panel has a blue background color.
- `secondaryBackgroundColor="#AED6F1"` - This sets the secondary background color to dark gray. Notice the gray background color of the sidebar and the background color of the code box in the main panel.
- `textColor="#FFFFFF"` - The text color is set to white.
- `font="monospace"` - This sets the font to monospace.

Figure10:

<img src="https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/image-20221103155537025.png" alt="image-20221103155537025" style="zoom: 33%;" />

## Further reading

- [Theming](https://docs.streamlit.io/library/advanced-features/theming)
- [HTML Color Codes](https://htmlcolorcodes.com/) is a great tool for selecting colors of interest.

# 🗓️ Day 17

#### st.secrets

`st.secrets` allows you to store confidential information such as API keys, database passwords or other credentials.

## Demo app

[![Streamlit App](https://johnyin.oss-cn-shanghai.aliyuncs.com/uPic/streamlit_badge_black_white-20221103160133751.svg)](https://share.streamlit.io/dataprofessor/st.secrets/)

## Code

Here's how to use `st.secrets`:

```python
import streamlit as st

st.title('st.secrets')

st.write(st.secrets['message'])
```

## Line-by-line explanation

The very first thing to do when creating a Streamlit app is to start by importing the `streamlit` library as `st` like so:

```python
import streamlit as st
```

This is followed by creating a title text for the app:

```python
st.title('st.secrets')
```

Finally, we'll be displaying the stored secrets:

```python
st.write(st.secrets['message'])
```

It should be noted that, secrets can be stored in Streamlit Cloud as shown in the screenshots shown below.

If working locally, they can be stored in `.streamlit/secrets.toml`, but make sure to avoid uploading this to a GitHub repo when deploying the app.

## Further reading

- [Add secrets to your Streamlit apps](https://blog.streamlit.io/secrets-in-sharing-apps/)
- [Secrets management](https://docs.streamlit.io/streamlit-cloud/get-started/deploy-an-app/connect-to-data-sources/secrets-management)
