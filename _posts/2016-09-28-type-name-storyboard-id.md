---
layout: post
title:  "Type Names as Storyboard IDs"
tags: 	xamarin ios tips storyboard xcode C#
excerpt: A while back I got in the habit of using the names my of custom types as different identifiers in iOS and macOS storyboards. This post looks at a couple examples of how this simple practice removes the need for unnecessary strings and leads to cleaner code.
---

##### _**Updated** on September 30, 2016 to use `nameof` operator added in C# 6 instead of `typeof`.  Thanks to [@glenntstephens][1] for the great suggestion!_


A while back I got in the habit of using the names my of custom types as different identifiers in iOS and macOS storyboards.

This post looks at a couple examples of how this simple practice removes the need for unnecessary strings and leads to cleaner code.


## Storyboard Identifier

In the first example I've added a new `UITableViewController` to my storyboard, set the Class to `CustomTableViewController` and the Storyboard ID to _"CustomTableViewController"_


![Xcode screenshot]({{ full_base_url }}/images/type-name-storyboard-id-0.png)


I can now programmatically create a new instance of `CustomTableViewController` using its Storyboard ID:


{% highlight c# %}
var storyboardId = "CustomTableViewController";
var controller = Storyboard.InstantiateViewController (storyboardId) as CustomTableViewController;
{% endhighlight %}


Everything works as expected, as long as I have a view controller in my storyboard with a matching Storyboard ID, and there isn't a typo in the string.


However, if I _know_ that the Storyboard ID is the same as the type's name, I can use the `nameof` operator and get rid of the string altogether:


{% highlight c# %}
var storyboardId = nameof(CustomTableViewController);
var controller = Storyboard.InstantiateViewController (storyboardId) as CustomTableViewController;
{% endhighlight %}


Or even better, write an extension method like this:


{% highlight c# %}
public static T Instantiate<T> (this UIStoryboard storyboard)
	where T : UIViewController
=> storyboard.InstantiateViewController (nameof (T)) as T;
{% endhighlight %}


And cut the code down to:


{% highlight c# %}
var controller = Storyboard.Instantiate<CustomTableViewController>();
{% endhighlight %}


Now, I not only got rid of the string identifier, but I'll also get build-time checking that my custom type inherits from `UIViewController`.


## Reuse Identifier

An even more common example of benefiting from this practice, is in the context of Reuse IDs on `UITableView` or `UICollectionView` cells.  Take the `UITableViewCell` subclass below.


{% highlight c# %}
public class CustomTableViewCell : UITableViewCell
{
	public void SetData(Item item) => titleLabel.Text = item?.Name;
}
{% endhighlight %}


In my storyboard, I've set the `CustomTableViewController`'s prototype cell's Class to `CustomTableViewCell`:


![Xcode screenshot]({{ full_base_url }}/images/type-name-storyboard-id-1.png)


Then set the cell's Reuse ID to _"CustomTableViewCell"_


![Xcode screenshot]({{ full_base_url }}/images/type-name-storyboard-id-2.png)


Normally, my `CustomTableViewController` (or `UITableViewDataSource`) `GetCell` override would look something like this:


{% highlight c# %}
public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
{
	var reuseId = "CustomTableViewCell";

	var cell = tableView.DequeueReusableCell (reuseId, indexPath) as CustomTableViewCell;

	cell?.SetData (Items [indexPath.Row]);

	return cell;
}
{% endhighlight %}


However again, if I _know_ that the Reuse ID is the same as the cell type's name, I can get rid of the string, and write another extension method:


{% highlight c# %}
public static T Dequeue<T> (this UITableView tableView, NSIndexPath indexPath)
	where T : UITableViewCell
=> tableView.DequeueReusableCell (nameof (T), indexPath) as T;
{% endhighlight %}


And cut my `GetCell` override to the code below, with the build-time checks:


{% highlight c# %}
public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
{
	var cell = tableView.Dequeue<CustomTableViewCell>(indexPath);

	cell?.SetData (Items [indexPath.Row]);

	return cell;
}
{% endhighlight %}


## Dig it?

You can find a the extension methods mention above and several more including support for collection views, [here][0].


[0]:https://github.com/colbylwilliams/NomadCode/blob/master/NomadCode/NomadCode.iOS/Extensions/StoryboardExtensions.cs
[1]:https://twitter.com/glenntstephens