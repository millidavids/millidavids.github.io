---
layout: post
title:  "Conway game of life (syntax test)."
date:   2015-01-24
categories: syntax highlight
---

Testing pygments syntax highlighting by passing in my Conway class.

{% highlight ruby %}
class Conway
  def initialize x, y
    @board = Array.new(x) { Array.new(y, 0) }
  end

  def activate_coordinate x, y
    @board[x][y] = 1
  end

  def deactivate_coordinate x, y
    @board[x][y] = 0
  end

  def evolve
    new_board = @board
    @board.length.times do |x|
      @board[0].length.times do |y|
        if @board[x][y] == 1 && active_neighbors(x, y) < 2
          new_board[x][y] = 0
        elsif @board[x][y] == 1 && active_neighbors(x, y).between?(2, 3)
          next
        elsif @board[x][y] == 1 && active_neighbors(x, y) > 3
          new_board[x][y] = 0
        elsif @board[x][y] == 0 && active_neighbors(x, y) == 3
          new_board[x][y] = 1
        end
        @board = new_board
      end
    end
  end

  private

  def active_neighbors x, y
    reach = [-1, 0, 1]
    neighbors = []
    count = 0
    reach.each do |x_reach|
      reach.each do |y_reach|
        next if [x + x_reach, y + y_reach] == [x, y]
        next if x + x_reach < 0 || x + x_reach >= @board.length
        next if y + y_reach < 0 || y + y_reach >= @board[0].length
        count += 1 if @board[x + x_reach][y + y_reach] == 1
      end
    end
    count
  end
end
{% endhighlight %}

---

{% highlight ruby %}
def signature
  "David Yurek".fancy_handwritingify
end
{% endhighlight %}
