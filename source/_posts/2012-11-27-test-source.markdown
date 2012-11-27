---
layout: post
title: "test_source"
date: 2012-11-27 14:31
comments: true
categories: 
---
``` ruby
class Fixnum
  def prime?
    ('1' * self) !~ /^1?$|^(11+?)\1+$/
  end
end
```


