using System;
using System.Collections.Generic;
using System.IO;
using System.Text.Json;
using System.Xml.Serialization;

namespace ConsoleSerialization_1
{
    class Program
    {
        public static void JSONReadDown()
        {

            IList<Person> persons = new List<Person>();
            string ObjectJSONfile = File.ReadAllText(nameJSONfile);
            persons = JsonSerializer.Deserialize<List<Person>>(ObjectJSONfile);

            foreach (Person person in persons)
            {
                Console.WriteLine($" Id = {person.id} \n Name = {person.Name}\n Surname = {person.SurName}\n Profession = {person.Profession}");
            }
        }

        public static void XMLReadDown()
        {
            XmlSerializer xmlSerializer = new XmlSerializer(typeof(List<Person>));
            using (FileStream fs = new FileStream("Persons.xml", FileMode.OpenOrCreate))
            {
                IList<Person> list = (List<Person>)xmlSerializer.Deserialize(fs);
                //Console.WriteLine("Получено из XML");
                foreach (Person person in list)
                {
                    Console.WriteLine($"ID: {person.id}\n Фамилия: {person.SurName}\n Имя: {person.Name}\n Профессия: {person.Profession}");
                }
            }
        }

        static void Main(string[] args)
        {
            Console.WriteLine("Процесс тестовой десериализации.");



            Console.WriteLine("JSON Deserialized: ");
            Console.WriteLine("--------------------------");
            JSONReadDown();

            Console.WriteLine("--------------------------");
            Console.WriteLine("XML Deserialized: ");
            Console.WriteLine("--------------------------");

            XMLReadDown();

            Console.WriteLine("--------------------------");

            Console.WriteLine("Объект десериализован!");
            Console.ReadKey();
        }

        private const string nameJSONfile = "TestFile.json";
        private const string nameXMLfile = "Person.xml";

    }

    public class Person
    {
        public int id { get; set; }
        public string SurName { get; set; }
        public string Name { get; set; }
        public string Profession { get; set; }

        public Person() { }
        public Person(int ID, string surname, string name, string profession)
        {
            this.id = ID;
            this.SurName = surname;
            this.Name = name;
            this.Profession = profession;
        } //не пригодилось. :/  



    }





}
