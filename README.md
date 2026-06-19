This R program simulates data from a nonlinear exponential model, estimates the unknown parameters using Nonlinear Least Squares (NLS), and visualizes the fitted curve.
# R-programing
#-----------------------------------------
# Simulation for nonlinear model
# y = a*exp(bx) + error
#-----------------------------------------

# Set seed for reproducibility
set.seed(123)

# Sample size
n <- 100

# True parameter values
a_true <- 2
b_true <- 0.5

#-----------------------------------------
# Generate X from a probability distribution
# Here: Normal distribution
#-----------------------------------------
x <- rnorm(n, mean = 1, sd = 1)

#-----------------------------------------
# Generate random errors
# Here: Normal distribution
#-----------------------------------------
error <- rnorm(n, mean = 0, sd = 0.5)

#-----------------------------------------
# Generate Y from nonlinear exponential model
#-----------------------------------------
y <- a_true * exp(b_true * x) + error

#-----------------------------------------
# Fit nonlinear regression model
#-----------------------------------------
model <- nls(y ~ a * exp(b * x),
             start = list(a = 1, b = 0.1))

#-----------------------------------------
# Display estimated parameters
#-----------------------------------------
summary(model)

# Estimated coefficients
coef(model)

#-----------------------------------------
# Plot data and fitted curve
#-----------------------------------------
plot(x, y,
     main = "Nonlinear Exponential Regression",
     xlab = "x",
     ylab = "y")

# Add fitted curve
x_grid <- seq(min(x), max(x), length = 200)

y_fit <- coef(model)[1] * exp(coef(model)[2] * x_grid)

lines(x_grid, y_fit, col = "blue", lwd = 2)
