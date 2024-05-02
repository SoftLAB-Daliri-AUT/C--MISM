# C--MISM
Multiplex maximum independent set
using System;
using System.Collections.Generic;

public class Node
{
    public int Id { get; set; }
    public List<Node> Neighbors { get; set; }

    public Node(int id)
    {
        Id = id;
        Neighbors = new List<Node>();
    }
}

public class MultiplexNetwork
{
    public List<List<Node>> Layers { get; set; }

    public MultiplexNetwork()
    {
        Layers = new List<List<Node>>();
    }

    public void AddLayer(List<Node> layer)
    {
        Layers.Add(layer);
    }

    public List<Node> FindMaximumIndependentSet()
    {
        List<Node> independentSet = new List<Node>();

        foreach (var layer in Layers)
        {
            foreach (var node in layer)
            {
                bool isIndependent = true;
                foreach (var neighbor in node.Neighbors)
                {
                    if (independentSet.Contains(neighbor))
                    {
                        isIndependent = false;
                        break;
                    }
                }
                if (isIndependent)
                {
                    independentSet.Add(node);
                }
            }
        }

        return independentSet;
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Create nodes and layers
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);

        List<Node> layer1 = new List<Node> { node1, node2 };
        List<Node> layer2 = new List<Node> { node3, node4 };

        // Add neighbors
        node1.Neighbors.Add(node2);
        node2.Neighbors.Add(node1);
        node3.Neighbors.Add(node4);
        node4.Neighbors.Add(node3);

        // Create multiplex network
        MultiplexNetwork network = new MultiplexNetwork();
        network.AddLayer(layer1);
        network.AddLayer(layer2);

        // Find maximum independent set
        List<Node> independentSet = network.FindMaximumIndependentSet();

        // Print the result
        Console.WriteLine("Maximum Independent Set:");
        foreach (var node in independentSet)
        {
            Console.WriteLine(node.Id);
        }
    }
}
