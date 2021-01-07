using System;


namespace Shape_Point
{
    public class Point
    {
        public int X { get; set; }
        public int Y { get; set; }

        public Point(int x, int y)
        {
            X = x;
            Y = y;
        }

        public override string ToString()
        {
            return "("+this.X + "," + this.Y+")";
        }

        public static double distanceTwoPoint(Point p1, Point p2)
        {
            double d = Math.Sqrt(Math.Pow(p2.Y - p1.Y, 2) + Math.Pow(p2.X - p1.X, 2));
            return d;
        }
    }

    public interface IShape1
    {
        void Perimeter(); 
    }

    public interface IShape2
    {
        void Area();
    }

    public class Triangle: IShape1, IShape2
    {
        private Point a, b, c;
        public Triangle(Point A, Point B, Point C)
        {
            this.a = A;
            this.b = B;
            this.c = C;
            
            if ((!Check()))
            {
                Exception exception = new Exception("Invalid");
                throw exception;
            }
        }

        public bool Check()
        {
            int check = a.X * (b.Y - c.Y) + b.X * (c.Y - a.Y) + c.X * (a.Y - b.Y);
            return check != 0;
        }

        public double Distance(Point A, Point B)
        {
            double distance = Point.distanceTwoPoint(A, B);
            return distance;
        }

        public double AB()
        {
            return Distance(a, b);
        }
        public double AC()
        {
            return Distance(a, c);
        }
        public double BC()
        {
            return Distance(b, c);
        }

        public void ShowEdge()
        {
            Console.WriteLine("3 edge of Triangle: {0} , {1} , {2} " , Math.Round(AB(),3) , Math.Round(AC(), 3) , Math.Round(BC(), 3));
        }

        public double A()
        {
            double CosA = (AC() * AC() + AB() * AB() - BC() * BC()) / (2 * AC() * AB());
            return Math.Acos(CosA);
        }
        public double B()
        {
            double CosB = (BC() * BC() + AB() * AB() - AC() * AC()) / (2 * AB() * BC());
            return Math.Acos(CosB);
        }
        public double C()
        {
            double CosC = (AC() * AC() + BC() * BC() - AB() * AB()) / (2 * AC() * BC());
            return Math.Acos(CosC);
        }

        public void ShowAngle()
        {
            Console.WriteLine("3 angle of Triangle: {0} , {1} , {2} ", Math.Round(A(), 3), Math.Round(B(), 3), Math.Round(C(), 3));
        }

        public double perimeter()
        {
            return AB() + BC()+ AC();
        }

        public double area()
        {
            double s1 = (b.X - a.X) * (c.Y - a.Y);
            double s2 = (c.X - a.X) * (b.Y - a.Y);
            double s3 = Math.Abs(s1 - s2) / 2;
            return s3;
        }

        public void Perimeter()
        {
            Console.WriteLine("Perimeter of Triangle: " + Math.Round(perimeter(),3));
        }
        public void Area()
        {
            Console.WriteLine("Area of Triangle: " + area());
        }

        public override string ToString()
        {
            return "3 points of triangle: " + a + " " + b +" " + c;
        }
    }

    public class Circle : IShape1, IShape2
    {
        private Point a;
        int Radius;
        public Circle(Point A, int radius)
        {
            this.a = A;
            this.Radius = radius;
            if (Radius < 0)
            {
                throw new Exception("the radius must be greater than 0");
            }
        }

        public double perimeter()
        {
            return 2 * Math.PI * Radius;
        }

        public double area()
        {
            return Math.PI * Radius * Radius;
        }

        public void Perimeter()
        {
            Console.WriteLine("Perimeter of Circle: " + Math.Round(perimeter(),3));
        }
        public void Area()
        {
            Console.WriteLine("Area of Circle: " + Math.Round(area(),3));
        }

        public override string ToString()
        {
            return "the circle has center " + a + " and radius = " + Radius;
        }

    }


    public class Rectangle : IShape1, IShape2
    {
        public double width { get; set; }
        public double height { get; set; }

        public Rectangle() { }
        public Rectangle(double width, double height)
        {
            if (width < 0 || height < 0) throw new Exception("side length must be greater than 0.");
            this.width = width;
            this.height = height;
        }

        public virtual double perimeter()
        {
            return 2 * (width + height);
        }

        public virtual double area()
        {
            return width * height;
        }

        public virtual void Perimeter()
        {
            Console.WriteLine("Perimeter of Rectangle: " + perimeter());
        }

        public virtual void Area()
        {
            Console.WriteLine("Area of Rectangle: " + area());
        }

        public override string ToString()
        {
            return "the rectangle has width = " + width + " and height = " + height;
        }

    }

    public class Square : Rectangle
    {
        public Square() { }
        public Square(double height)
        {
            base.height = base.width = height;
        }

        public Square(double height, double width) : base(height, width)
        { }

        public override double perimeter()
        {
            return 4 * this.height;
        }

        public override double area()
        {
            return height * height;
        }

        public override void Perimeter()
        {
            Console.WriteLine("Perimeter of Square: " + perimeter());
        }

        public override void Area()
        { 
            Console.WriteLine("Area of Square: " + area());
        }

        public override string ToString()
        {
            return "the square has width = " + height;
        }

    }

    public class Pentagon : IShape1
    {
        private double x1,x2,x3,x4,x5;
        public Pentagon(double x1, double x2, double x3, double x4, double x5)
        {
            this.x1 = x1;
            this.x2 = x2;
            this.x3 = x3;
            this.x4 = x4;
            this.x5 = x5;
            if (x1 < 0 || x2 < 0 || x3 < 0 || x4 < 0 || x5 < 0) throw new Exception("side length must be greater than 0.");
        }

        public double perimeter()
        {
            return x1 + x2 + x3 + x4 + x5;
        }

        public void Perimeter()
        {
            Console.WriteLine("Perimeter of Pentagon: " + perimeter());
        }

        public override string ToString()
        {
            return "the pentagon has 5 edges : " + x1 + " " + x2 + " " + x3 + " " + x4 + " " + x5;
        }

    }


    class Program
    {
        static void Main(string[] args)
        {
            Point A = new Point(2, 3);
            Point B = new Point(2, 4);
            Point C = new Point(4, 6);

            Triangle triangle = new Triangle(A, B, C);
            Console.WriteLine(triangle.ToString());
            triangle.ShowAngle();
            triangle.ShowEdge();
            triangle.Perimeter();
            triangle.Area();
            Console.WriteLine("--------------------------------------------------------------------");
            Console.WriteLine();

            Circle circle = new Circle(A, 3);
            Console.WriteLine(circle.ToString());
            circle.Perimeter();
            circle.Area();
            Console.WriteLine("--------------------------------------------------------------------");
            Console.WriteLine();

            Rectangle rectangle = new Rectangle(3, 4);
            Console.WriteLine(rectangle.ToString());
            rectangle.Area();
            rectangle.Perimeter();
            Console.WriteLine("--------------------------------------------------------------------");
            Console.WriteLine();

            Square square = new Square(2);
            Console.WriteLine(square.ToString());
            square.Perimeter();
            square.Area();
            Console.WriteLine("--------------------------------------------------------------------");
            Console.WriteLine();

            Pentagon pentagon = new Pentagon(1, 2, 3, 4, 5);
            Console.WriteLine(pentagon.ToString());
            pentagon.Perimeter();



        }
    }
}
