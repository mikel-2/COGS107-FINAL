# COGS107-FINAL

SDT & Diffusion Modeling Analysis

This final project will analyze certain simulated response times and accuracy data from a 2×2×2 experimental design using 2 common modeling approaches Signal Detection Theory (SDT) and the Diffusion Decision Model (DDM)

# The goals  
1. To quantify the effects of 'stimulus complexity' and the trial difficulty on a subjects performance  
2. Fit a hierarchical bayesian model to estimate d_prime sensitivity and bias (in c)  
3. Generate delta plots to show response time distrubution  

# AI Usage  
I used ChatGPT for code writing suggestions as well as to help me understand concepts of these models and analyses.  

## Steps and helpful info on how to re-run/adjust code easily  

You can change parameters in the script to rerun the models with different configurations or datasets.  

1. Change number of posterior samples (for speed vs. precision)  
Inside pm.sample(...):  
trace = pm.sample(draws=2000, tune=1000, target_accept=0.95)  
-+-+-+-+-+-  
draws: number of posterior samples to retain  
tune: number of warm-up steps (used for adaptation, not stored)  
target_accept: helps prevent divergences (higher = more cautious, e.g., 0.95)  

2. Change which participants get delta plots  
for pid in [1, 2, 3]:  # Only plot for selected participants  
    draw_delta_plots(df_delta, pnum=pid)  
-+-+-+-+-+-  
Replace the list [1, 2, 3] with any subset you want  
Or use .sample(n=3) to pick random ones  

3. Change credible interval width in posterior plots  
Control the width of the credible interval:  
az.plot_posterior(trace, hdi_prob=0.9)  
-+-+-+-+-+-  
hdi_prob: set to 0.9 for 90%, 0.99 for 99%, etc.  
Affects interpretation of uncertainty  

4. Load a different dataset  
Just place a new file named data.csv inside the data/ folder. The code automatically reads:  
df = pd.read_csv(Path(__file__).parent.parent / 'data' / 'data.csv')  
-+-+-+-+-+-  
Make sure the new dataset uses the same column structure and naming.
