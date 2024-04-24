# rinterface-wasm-cran

From George Stagg:

> In Shinylive, there is some startup code to search for dependencies in an app and automatically install them before the app has loaded. With this, users do not need to know about webr::install(). However, the code does not take into account downloading from alternative repositories. I have opened an issue about it here: posit-dev/shinylive#125.

> For the moment, while far from ideal, there should be a workaround in removing the automatically installed version of shinyMobile before running webr::install():

```r
webr::unmount("/usr/lib/R/library/shinyMobile")
webr::install(
  "shinyMobile",
  repos = c("https://rinterface.github.io/rinterface-wasm-cran/", "https://repo.r-wasm.org")
)
```

See [example](https://shinylive.io/r/editor/#code=NobwRAdghgtgpmAXGKAHVA6ASmANGAYwHsIAXOMpMAdzgCMAnRRAVwhiLdIAoAdMAPQsAzgwEAbAJZ0BWCdIZQGATwHCAFpIjKAskTqTxcfgEpeEWo2ZbhpKOPF8IAAmf8NW3fsPG851wxwqETCzgC8zgR8YOqkpKjCiAICDFrkDABmUARwGADmkqTqLHQYkkQpaXCZ2XAAtNRQwjB1BIoQAvy4bjFxCUkpQUQYDA1NMBhEDHmm5mYQ5lKMSsrcHtrzAMTOAHJwcAAmoVDOwqhwBJIZkgTOAG7VwuUuRBnOjEQExYHOGVPOECI1Aw5m2ABVNMcHEDQqQiM5UE1QtRFOhqr82ARSM9kYV1M4iKhsSRhKDnE1nFJbBhnAB1OAA-YHZyFd4XKAiBmvZxFBkZADsAAUoHkuUScQilLA4OkyVAIMy4ZLhLD1AyGJxyKEqaQCXQAFYXXV-BjOABSAGUQRBtgc4Hc4URxIlEDY7A4APoFIolaIAEUkdygBx2RH10GmAg+XxYgVmECWihU3Gj3zg80TKzWmm0egMRnmiy0AGtQgAeOqUtCocSrABMiAAzN0MpjiRBuJITM4QP4eSLhAASKROVyuAUAGRLo7HAU1UDoRnCzjBWAAqgBRXB92fiBdwcTLs6pMgZaJTiDFnnwxGi5wAUlJeBZJm3LlnznUgTeEWPaTP-ACI+XQvjuzjzK48wAL6FhAt5wB6ACMzgVhiEBYs83Ddr277wTOrhfnAP49J0fjvq4LCSMurboe23CBAAjiwcC2NhYGuOsyjMHYeRDgcgb4R+BB7iqy78PBXTsWO2xwqgAJQHcdBKM4eRECxn7VMY5EfgKOwKUpDDcNipBLhE-AABJEPAkqiqYb4fmOPF8QJUmzsJSJiWA8GtCQ5BkJJ2kOZOki2IJDmuDYMrLqum72eFs62BqEB5NF65bq5H6alIEAMhEMXpYF4X8Xckh2gwoR5WlcXxa4HB2p52WlgFNVjo1pKFbOEHhV1nVgVBfbQeY5jwR6dYoZWNEYSQWE9n2eFgYRxGAXWzVjpR1FtphjHMaxs2FZx3EDoOxVhWO7miWZXkir41UfjJhLyYpymqepapxh1vz8npT2GRlrjGaZPQWhcJDMhJZEtdsACC0LULC8Kqe82RXkqMBQFof2UkRpDCjlh4RE5g5QKdDmLZ5pG3fF50VT0jWrS1hOSNw1OeTcJAssQEB1EpBDFnZmP-UdZzyiT4Us5dVx1ICpB1DABz0y1PQAELI-wAvgZjPUfq+GXbDsADyYIbogzjUGqLi8s4aNaNeToGSyoQUAuRjMhjH3bAKOgsOI2ITlAyiat0tCRPKADkuqciyCqBqVLD2DZDKOuIBnCNa8Ue-yYJEHbSii9sCIhIUzyeXQRBxFZCuzvnhPE7rs5k5dFN12O-A6OjLjg5T0luSJNP8HTYDN1rVfgV3HE5lxiCEydmPiz03mc35pCVzp-JK+InzFtwApKyw5cdloqB7wAksyl0sKgBxQOQIF7nQB6eWul-XwythBOcDCmDrH3jvyU6herRKJAUqVViurSKupQEFUVgSPe2VcrOAAGJQwnBaaBisBQWnIGiX6P8PyHxPmfHob8cEr3infB+l0dDKFONgj+ZDwowBthEAADGPRhUAAAey5EJsPVhxSQAAvBB7g0YOAYQ5IM4hmLLgACzsIciiNANN8oKI-ByOEgRzjX1SmAvBs4NRsDtEQ5BqD0EwMUCFQ4y5TFoLUbONGEA474yQSgtB6th7azUQ8BgSlsQwDBHAThpB9Z7yPjwfgWpl5gE8ZBKSWt+rvkGgsOC10PSNnGmhKaHY2K4WuoJBuJFGwK3WhESadFtosVILkhyB0p5HRnh9Oe4lroMPunJaAP0VJqVCG9LS8VdL6VzpjAGIiwAQkkAwMGrSIY1WhrDeG3Ska82vFbdumMjAZBxvKSh-ZeJE1FvXb85MJFnV7g1EspzBb7KZs0sAbMXAPO5qrGJ9i9lDmFh2fhkRzkSwyFLMust5azJgfwFWvM1b6I1ng2Jo864GyNibM2FAeRqjWTbJO9sQrOCdouaxbt06fS9j7SQfsA57yDgyAgYcI7CAZFoYqsd47wVtsnJQqc64CizjnXBhKC5PHbCXMucIYBtOuUOWu7sjlEXJitEFd1Zz8GBpzaZtl5UjzOR5S6A8h512-vFOp08XJ4LuQvXyFBolqJ3hvXm0RQxFC0ClJUGggTOGUFFDAnr4zxU8Qkga5hEnmFTLGOAUN0Azm2MKUU7VXAjUQlhOKI06wJrmmkxsKb3zbGPjAYIDA7BkBNhitUUwaHBp+GjYsLE+zbDgNkfELL1AKUdSyUgoQgQuE4qcFiTwSACC7QwHxWT2xp2cOCRtpBQ6hGlqbcdpsGSNDIBpH4wh4S0FDg4T8Cl+mjvJCpDeSlDx0oHeicpzwR1HsHWUza00CGkG6JqcJ3Q6UqmeDUscD696DkCOWSsgQFTVECcEzscFP3kGCVrD9pBBxRMyX+sqgoTw8FvYOEhH9YKzn0BeuAG4HhkGA+EwcF8r7kG6DhByRGX6IP5Fg9+1RRa3tPp5VD1QGFSJkawjAiF2EkOXCwjALCuMZSeMIhqSg1XsKYS4VhEmuE8PYUohINi3HmPUXvKYQRa2QNcWY9hhj-1ENURlSxdKDNVQysQDeppLqoEueqscjjnG6JU7OO0lwxGCiIGkZcK1CoJK6lBOKCnzhEM9t7X2-tA59iC4cD0hJ2w0x1IJbYABhKyHALbZzZZ-bSmLlJlMzplgyp1gqXk7Jzai-Jj6c2iOoTgdK7KfmOY3EChi7B4qc1rfV77xQkmXIlqSV8GBXigV3Xk1lLpyxXq19SER+sfUS4iIoJznyxhcYBEC0Bxs9Fq-AfmUrs25vzaQE2BwSDh2cIEDgDxnCVqCPYQM26HIe3+F8Qwqr1IUgdVCDecM67Oq3ai+lIHdS2BfjOlFwhqCFFe8lOu99SC0BRfBVOzhj5vFsVuHFdaeSSGsicFlIU65fHlKKA43Rb3HB+N+qK3Agk5CJASC2aLrjlV1PBEwI6HILevviRucruirdlRt6Unl+c3f2KgGGD2OvsO50txuxSVsMDW4IRX3RNtjLV+LoIUvrtQN9WBLq8wTBgCggAXSAA).
