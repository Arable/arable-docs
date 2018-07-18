---
title: Wrangling Data
keywords: coding
summary: "Learn how to slice and dice data"
sidebar: examples_sidebar
permalink: ex2_Wrangling.html
simple_map: true
map_name: usermap
box_number: 2
folder: examples
---

## Introduction

Once data is stored as a dataframe, there are many nuts-and-bolts operations to add new columns, drop columns, resample data, aggregate data, join multiple tables, concatenate rows, and the like.  

We use the [pandas](https://pandas.pydata.org/) framework for handling data, chiefly because it has a lot of built-in functions for handling data like ours, which is to say time-indexed multivariate data.

## Working with indices

	Calculating a local time (get time offset from locations api)

	Calculating a solar time

## Inner join, e.g. with health (example rssi versus rain)

## Outer join, forward fill (e.g. for a custom kc)

## Diurnal temperature range


## Groupby, resample, sum to get daily or weekly metrics
https://stackoverflow.com/questions/45281297/group-by-week-in-pandas

## Concatenate multiple devices - weekly report
