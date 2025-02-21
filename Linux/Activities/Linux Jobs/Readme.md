# Ensure fixGenerator.sh is in the home directory
mv fixGenerator.sh ~/fixGenerator.sh

# Run Monday–Friday at 6am 
0 6 * * 1-5 ~/fixGenerator.sh

# Run at 6pm every Friday
0 18 * * 5 ~/fixGenerator.sh

# Run every half hour from 9–4 on Monday, Wednesday, and Friday
*/30 9-16 * * 1,3,5 ~/fixGenerator.sh

# Run every other hour every day
0 */2 * * * ~/fixGenerator.sh

# Run on May 4th at midday
0 12 4 5 * ~/fixGenerator.sh

# Run on the 1st of every month at 6:25am
25 6 1 * * ~/fixGenerator.sh

# Run every 20 minutes every Tuesday between 10am and 2pm
*/20 10-14 * * 2 ~/fixGenerator.sh

# Run the 1st of every other month on the hour
0 * 1 */2 * ~/fixGenerator.sh

# Run at 6am and 8am on Saturday and Sunday
0 6,8 * * 6,0 ~/fixGenerator.sh

# Copy the crontab contents to a file in the scripts folder
crontab -l > ~/scripts/crontab_backup.txt
