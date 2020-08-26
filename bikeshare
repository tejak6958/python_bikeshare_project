import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }
days_in_week = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday', 'All']
months = ['January', 'February', 'March', 'April', 'May', 'June', 'All']
def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # TO DO: get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    while True:
        city = input('Would you like to see data from Chicago, New York City, or Washington? ').lower()
        if city in ('chicago', 'new York City', 'washington'):
            print('\nYou selected {}.'.format(city))
            break
        else:
            print('\nPlease, you must enter one of the three cities in the promp as it is written')

    # TO DO: get user input for month (all, january, february, ... , june)
    while True:
        month = input('\nFor which month, January through June, would you like to see data? If you want to see data for all six month, type all. ').title()
        if month in months:
            print('You selected {}.'.format(month))
            month = months.index(month) + 1
            break
        else:
            print('\nPlease, check your writing. If you want to see data for all six month, type all. ')


    # TO DO: get user input for day of week (all, monday, tuesday, ... sunday)
    while True:
          day = input('\nFor which day of the week would you like to have more details? If you want to see data for all seven days, type all. ').title()
          if day in days_in_week:
            print('You selected {}.'.format(day))
            break
          else:
            print('\nPlease, check your writing. Enter the day without abreviations (i.e. Sunday). If you want to see data for all seven days of week, type all. ')

    print('-'*40)
    return city, month, day


def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
    df = pd.read_csv(CITY_DATA[city])
    # Convert the Start TIme column to datetime
    df['Start time'] = pd.to_datetime(df['Start Time'])
    # Extract month and day of week from Start Time
    df['month'] = df['Start time'].dt.month
    df['day_of_week'] = df['Start time'].dt.weekday_name
    #Filter by month if applicable
    if month != 'len(months)':
        # Filter by day of week to create the new dataframe
        df = df[df['day_of_week'] == day.title()]
    return df

def time_stats(df):
    """Displays statistics on the most frequent times of travel."""
    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # TO DO: display the most common month
    pop_month = df['month'].mode()[0]
    pop_month = months[pop_month -1]
    print('Most popular month: {}.'.format(pop_month))

    # TO DO: display the most common day of week
    pop_day_of_week = df['day_of_week'].mode()[0]
    print('Most popular day of week: {}.'.format(pop_day_of_week))


    # TO DO: display the most common start hour
    df['Start Time'] = pd.to_datetime(df['Start Time'])
    df['hour'] = df['Start Time'].dt.hour
    pop_hour = df['hour'].mode()[0]
    print('Most popular hour: {}.'.format(pop_hour))


    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # TO DO: display most commonly used start station
    pop_start = df['Start Station'].mode()[0]
    print('Most popular station to start a trip: {}'.format(pop_start))

    # TO DO: display most commonly used end station
    pop_end = df['End Station'].mode()[0]
    print('Most popular station to end a trip: {}'.format(pop_end))

    # TO DO: display most frequent combination of start station and end station trip
    df['trip'] = df['Start Station'] + ' to ' + df['End Station']
    pop_trip = df['trip'].mode()[0]
    print('Most popular trip: {}.'.format(pop_trip))

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # TO DO: display total travel time
    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # TO DO: display mean travel time
    tot_travel_time = df['Trip Duration'].sum()
    print('The total of all trip durations is: {:.2f} minuts.'.format(int(tot_travel_time)/60))


    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # TO DO: Display counts of user types
    num_subscribers = df['User Type'].str.count('Subscriber').sum()
    num_customers = df['User Type'].str.count('Customer').sum()
    print('Number of subscribers are {}'.format(int(num_subscribers)))
    print('Number of customers are {}'.format(int(num_customers)))

    # TO DO: Display counts of gender

    if 'Gender' in df.columns:
        male_count = df['Gender'].str.count('Male').sum()
        female_count = df['Gender'].str.count('Female').sum()
        nan_num = df['Gender'].isnull().sum()
        print('\nNumber of male users are {}'.format(int(male_count)))
        print('Number of female users are {}'.format(int(female_count)))        
        print('{} people did not specify their gender'.format(int(nan_num)))
    else:
        print('This city does not have gender data.')

    # TO DO: Display earliest, most recent, and most common year of birth
    if 'Birth Year' in df.columns:
        print('\nThe birth year statistics:\n')
        print('The most recent birth year on the record is {}.'.format(int(df['Birth Year'].max())))
        print('The earliest recent birth year on the record is {}.'.format(int(df['Birth Year'].min())))
        print('The common recent birth year on the record is {}.'.format(int(df['Birth Year'].mode()[0])))
        print("\nThis took %s seconds." % (time.time() - start_time))
        print('-'*40)

    while True:
        word = input("Please enter 'Y' if you like to see 5 more: ")
        if word == "Y":
          print('display five more rows')
        else:
         print("Finished.")

def main():
   while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df)
        restart = input('\nWould you like to restart? Enter yes or no.\n')      
        if restart.lower() != 'yes':        
           break
        else:
             print('end')


if __name__ == "__main__":
	main()
# Online Python compiler (interpreter) to run Python online.
# Write Python 3 code in this online editor and run it.

print("Hello world")
