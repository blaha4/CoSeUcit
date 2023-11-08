# CoSeUcit
csharp




////
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace _8._11
{
    public class Aquarium
    {
        private int volume;
        private double phWater;
        private int temperatureWater;
        private WaterType waterType;
        private int capacity;

        private List<Fish> fishList = new();

        public Aquarium(int volume, double phWater, int temperatureWater, WaterType waterType, List<Fish> fishList)
        {
            this.volume = volume;
            this.phWater = phWater;
            this.temperatureWater = temperatureWater;
            this.waterType = waterType;
            this.fishList = fishList;
            capacity = volume;
        }

        public bool Add(Fish fish) 
        {
            //ify by bylo vhodnejsi nahradit metodami
            if (fish.Water != waterType) 
            {
                return false;
            }
            if (capacity - fish.Size < 0) 
            {
                return false;
            }
            if(!fish.Temperature.Contains(temperatureWater)) 
            {
                return false;
            }
            if(!fish.Ph.Contains(phWater)) 
            {
                return false;
            }
            fishList.Add(fish);
            capacity -= fish.Size;
            return true;
        }
    }
}

//////



///////////

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace _8._11
{
    public class Range<T> where T : IComparable<T>
    {
        private T min;
        private T max;
        public Range(T min, T max) 
        {
            this.min = min;
            this.max = max;
        }
        public static Range<T> Create(T min, T max) 
        {
            if (max.CompareTo(min) < 0) 
            {
                throw new ArgumentException("chyba");
            }
            return new Range<T>(min, max);
        }

        public override string ToString()
        {
            return $"<{min},{max}>";
        }

        public bool Contains(T value) 
        {
            return value.CompareTo(min) >= 0 
                && value.CompareTo(max) <= 0;
        }
    }
}


////////
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace _8._11
{
    public enum WaterType
    {
        FreshWater, Brackish, SaltWater
    }
    public class Fish
    {
        private int size;
        private string name;
        private Range<double> ph;
        private Range<int> temperature;
        private WaterType water;

        public Fish(int size, string name, Range<double> ph, Range<int> temperature, WaterType water)
        {
            this.size = size;
            this.name = name;
            this.ph = ph;
            this.temperature = temperature;
            this.water = water;
        }

        public int Size { get => size; set => size = value; }
        public string Name { get => name; set => name = value; }
        public Range<double> Ph { get => ph; set => ph = value; }
        public Range<int> Temperature { get => temperature; set => temperature = value; }
        public WaterType Water { get => water; set => water = value; }
    }
}
